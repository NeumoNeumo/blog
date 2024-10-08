---
title: "Comprend Drop Check with Simple Examples"
date: 2024-10-08T14:11:21+08:00
draft: false
categories: ["Program"]
tags: ["Rust", "drop", "tutorial"]
---

# Concepts in Drop Check

- What's the drop glue?
- Why do we need `#[may_dangle]`?
- In which case is a `PhantomData` necessary?

If you don't know the answer the questions above, this post would show you the
answers by concrete examples.

[This page](https://doc.rust-lang.org/nomicon/dropck.html) and [this
page](https://doc.rust-lang.org/nomicon/phantom-data.html) in Rustonomicon and
[this page](https://rust-lang.github.io/rfcs/1238-nonparametric-dropck.html) in
the RFC book may be helpful to you. But if you find them difficult to understand
like what I feel about them or too cumbersome and abstract, this post is what
you want. Additionally, reading materials from different sources has a synergic
effect. So although I believe this post is enough, you are encouraged to turn to
other resources like those links I mentioned above if you are stuck in some part
of the post. Leave me a comment when you encounter those moments. I will try to
improve it.

The code and comments are available in [this
repository](https://github.com/NeumoNeumo/ComprehendDropCheck). If you prefer to
take an adventure yourself, pull it down and play with it. All the following
texts here are included in the source file.

## Drop Order

Simply put: declared first, drop last.

```rust
fn drop_order() {
    struct A();
    struct B();
    impl Drop for A {
        fn drop(&mut self) {
            println!("A is dropped last because its declaration is the first")
        }
    }
    impl Drop for B {
        fn drop(&mut self) {
            println!("B is dropped first although its initialization is earlier than A");
        }
    }
    let a;
    let b = B();
    a = A();
}
```

```text
output:
B is dropped first although its initialization is earlier than A
A is dropped last because its declaration is the first
```

## Drop Glue

The destructor in rust consists of two parts to help us automatically drop all
the resources owned by the object:

 - the programmer customized function `Drop::drop`
 - Drop glue that the compiler automatically attached for us

```rust
#[allow(unused)]
fn drop_glue1() {
    struct A(B1, B2);
    struct B1();
    struct B2();
    impl Drop for A {
        // Even if you don't have a drop implementation, drop glue still applies to release the
        // resources of its members. But here we have an explicit implementation though.
        fn drop(&mut self) {
            println!("Drop for A called");
            // It is like the compiler automatically attaches sub-drop routine
            // at the end of the drop using "glue".
            println!("The following is the drop glue of A");
        }
    }
    impl Drop for B1 {
        fn drop(&mut self) {
            println!("Drop for B1 called as part of the drop glue of A");
            println!("No drop glue for B1 since it has no field");
        }
    }
    impl Drop for B2 {
        fn drop(&mut self) {
            println!("Drop for B2 called as part of the drop glue of A");
            println!("No drop glue for B2 since it has no field");
        }
    }

    A(B1(), B2());
}
```

```text
output: 
Drop for A called
The following is the drop glue of A
Drop for B1 called as part of the drop glue of A
No drop glue for B1 since it has no field
Drop for B2 called as part of the drop glue of A
No drop glue for B2 since it has no field
```

A drop glue only sticks OWNED members. If a member is a reference, the resources
of it should be managed by its owner instead of the borrower. In simple words,
who owns it drops it.

```rust
fn drop_glue2() {
    struct A<'a>(&'a B1, B2);
    struct B1();
    struct B2();
    impl<'a> Drop for A<'a> {
        fn drop(&mut self) {
            println!("Drop for A called");
        }
    }
    impl Drop for B1 {
        fn drop(&mut self) {
            println!("Drop for B1 called NOT as part of the drop glue of A");
            println!("Instead, this is called because its owner b1 is dropped");
        }
    }
    impl Drop for B2 {
        // I'm called as part of drop glue of A.
        fn drop(&mut self) {
            println!("Drop for B2 called as part of the drop glue of A");
        }
    }

    let b1 = B1();
    A(&b1, B2());
}
```

```text
output
Drop for A called
Drop for B2 called as part of the drop glue of A
Drop for B1 called NOT as part of the drop glue of A
Instead, this is called because its owner b1 is dropped
```

The drop glue can process recursively if the owned member also owns a member

```rust
fn drop_glue3() {
    struct A(B1);
    struct B1(C1, C2);
    struct C1();
    struct C2();
    impl Drop for A {
        fn drop(&mut self) {
            println!("Drop for A called");
        }
    }
    impl Drop for B1 {
        fn drop(&mut self) {
            println!("Drop for B1 as part of the drop glue of A");
            println!("because the ownership of b1 is transferred to A")
        }
    }
    impl Drop for C1 {
        fn drop(&mut self) {
            println!("Drop for C1 as part of the drop glue of B1");
        }
    }
    impl Drop for C2 {
        fn drop(&mut self) {
            println!("Drop for C1 as part of the drop glue of B1");
        }
    }

    let b1 = B1(C1(), C2());
    A(b1);
}
```

```text
output
Drop for A called
Drop for B1 as part of the drop glue of A
because the ownership of b1 is transferred to A
Drop for C1 as part of the drop glue of B1
Drop for C1 as part of the drop glue of B1
```

For more details about how drop glue works, you may check [the standard
library](https://doc.rust-lang.org/std/ops/trait.Drop.html#drop-check).

The gist is excerpted here. The *last rule* is very important.

> Currently, the analysis works as follows:
> - If T has no drop glue, then trivially nothing is required to be live. This
>   is the case if neither T nor any of its (recursive) fields have a destructor
>   (impl Drop). PhantomData and ManuallyDrop are considered to never have a
>   destructor, no matter their field type.
> - If T has drop glue, then, for all types U that are owned by any field of T,
>   recursively add the types and lifetimes that need to be live when U gets
>   dropped. The set of owned types is determined by recursively traversing T:
>   - Recursively descend through PhantomData, Box, tuples, and arrays
>     (including arrays of length 0).
>   - Stop at reference and raw pointer types as well as function pointers and
>     function items; they do not own anything.
>   - Stop at non-composite types (type parameters that remain generic in the
>     current context and base types such as integers and bool); these types are
>     owned.
>   - When hitting an ADT with impl Drop, stop there; this type is owned.
>   - When hitting an ADT without impl Drop, recursively descend to its fields.
>     (For an enum, consider all fields of all variants.)
> - Furthermore, if T implements Drop, then all generic (lifetime and type)
>   parameters of T must be live.

## May Dangle

When `drop` is not explicitly implemented for a type, only drop glue would run.
The compiler does not check the lifetime for potentially dangling reference
fields because we can definitely ensure that we would not access these reference
fields during dropping. We do access owned members though. But that's fine
because we have full privilege over it. We may call this kind of drop without
implementation as `trivial drop`.

```rust
fn may_dangle1() {
    struct A<'a>(&'a B);
    struct B(i32);
    impl Drop for B {
        fn drop(&mut self) {
            println!("B dropped here");
        }
    }

    let a;
    let b = B(42);
    a = A(&b);
    drop(b); 
    println!("&b dangles henceforth");
    println!("a would be dropped after this line");
    // The dangling &b doesn't matter because this is a trivial drop which means we will
    // not visit &a in destruction at all. So the compiler lets it go.
}
```

```text
B dropped here
&b dangles henceforth
a would be dropped after this line
```

When drop is explicitly implemented for a type, it requires this type outlives
its reference even though it is not necessary to do that semantically.

```rust
fn may_dangle2() {
    struct A(i32);
    struct B<'a>(&'a A);
    impl<'a> Drop for B<'a> {
        fn drop(&mut self) {
            // even do nothing here
        }
    }

    let mut b;
    let a = A(42);
    b = B(&a);

    // a gets dropped here
    // b gets dropped here. a does not live long enough but we will not deref &a. So it should be
    // OK effectively. But our compiler doesn't buy it.
}

```

```text
error[E0597]: `a` does not live long enough
   --> src/main.rs:188:11
    |
187 |     let a = A(42);
    |         - binding `a` declared here
188 |     b = B(&a);
    |           ^^ borrowed value does not live long enough
...
193 | }
    | -
    | |
    | `a` dropped here while still borrowed
    | borrow might be used here, when `b` is dropped and runs the `Drop` code for type `may_da
ngle2::B`
    |
    = note: values in a scope are dropped in the opposite order they are defined

For more information about this error, try `rustc --explain E0597`.
```

`#[may_dangle]` hints the compiler not to check the lifetime/borrow of 'a

```rust
fn may_dangle3() {
    struct A(i32);
    struct B<'a>(&'a A);
    unsafe impl<#[may_dangle] 'a> Drop for B<'a> {
        fn drop(&mut self) {
            // nothing here
        }
    }

    let mut b;
    let a = A(42);
    b = B(&a);
    // a gets dropped here
    // b gets dropped here. But #[may_dangle] makes it compiles.
}
```

```text
output
A dropped
B dropped
```

But if we explicitly call the drop, the borrow check would raise an compile error.

```rust
fn may_dangle3() {
    struct A(i32);
    struct B<'a>(&'a A);
    impl Drop for A {
        fn drop(&mut self) {
            println!("A dropped");
        }
    }
    unsafe impl<#[may_dangle] 'a> Drop for B<'a> {
        fn drop(&mut self) {
            println!("B dropped");
        }
    }

    let mut b;
    let a = A(42);
    b = B(&a);
    drop(a);
    drop(b);
}
```

```text
error[E0505]: cannot move out of `a` because it is borrowed
   --> src/main.rs:216:10
    |
214 |     let a = A(42);
    |         - binding `a` declared here
215 |     b = B(&a);
    |           -- borrow of `a` occurs here
216 |     drop(a);
    |          ^ move out of `a` occurs here
217 |     drop(b);
    |          - borrow later used here
    |
```

`#[may_dangle]` can be used to modify generics (after all, lifetime annotation is
a variety of generics)

```rust
fn may_dangle4() {
    struct A(i32);
    struct B<T>(T);
    impl Drop for A {
        fn drop(&mut self) {
            println!("A dropped");
        }
    }
    unsafe impl<#[may_dangle] T> Drop for B<T> {
        // impl<T> Drop for B<T> { // What happens if you uncomment this line?
        fn drop(&mut self) {
            println!("B dropped");
        }
    }

    let mut b;
    let a = A(42);
    b = B(&a);
    // a gets dropped here
    // b gets dropped here. But #[may_dangle] makes it compiles.
}
```

```text
output
A dropped
B dropped
```

`#[may_dangle]` is unsafe which means you need to ensure that you would not use
deref &A to avoid undefined behaviors.

```rust
fn may_dangle5() {
    struct B<T: Debug>(T);
    unsafe impl<#[may_dangle] T: Debug> Drop for B<T> {
        fn drop(&mut self) {
            // Warning! You told the compiler that you would not use T again but you did!
            println!("{:?}", self.0);
        }
    }

    let mut b;
    let a = Box::new(42);
    b = B(&a);
    // a gets dropped here
    // b gets dropped here. But #[may_dangle] makes it compiles.
}
```

You'd probably get a random number other than 42. It is 0 with my system alloc.
It may remains 42 with jemalloc. But that is not guarenteed in general.

```text
output
0
```

`#[may_dangle]` only applies to compiler-generated drop. If you drop variables
explicitly, drop checks still remain. This case is same as that for
`#[may_dangle]` a lifetime.

```
#[allow(unused)]
fn may_dangle6() {
    struct B<T: Debug>(T);
    unsafe impl<#[may_dangle] T: Debug> Drop for B<T> {
        fn drop(&mut self) {
            // nothing here
        }
    }

    let mut b;
    let a = Box::new(42);
    b = B(&a);
    drop(a);
    drop(b);
}
```

```text
error[E0505]: cannot move out of `a` because it is borrowed
   --> src/main.rs:283:10
    |
281 |     let a = Box::new(42);
    |         - binding `a` declared here
282 |     b = B(&a);
    |           -- borrow of `a` occurs here
283 |     drop(a);
    |          ^ move out of `a` occurs here
284 |     drop(b);
    |          - borrow later used here
    |
help: consider cloning the value if the performance cost is acceptable
    |
282 |     b = B(&a.clone());
    |             ++++++++
```

The following is another example of `#[may_dangle]` that shows this hint only
applies in compileer-generated drop. Dropping the owned  or referenced field
directly in your code makes it so dangerous that rustc decides not to indulge
`#[may_dangle]`.

```rust
#[allow(unused)]
fn may_dangle7() {
    struct A();
    struct B<T>(T); // T, which turns out to be A, is owned by B
    unsafe impl<#[may_dangle] T> Drop for B<T> {
        fn drop(&mut self) {
            println!("B dropped");
        }
    }
    impl Drop for A {
        fn drop(&mut self) {
            println!("A dropped as part of the drop glue of B");
        }
    }

    let mut b;
    let a = A();
    b = B(a);
    // Explicitly dropping a breaches the ownership system.
    drop(a);
}
```

```text
error[E0382]: use of moved value: `a`
   --> src/main.rs:310:10
    |
307 |     let a = A();
    |         - move occurs because `a` has type `may_dangle7::A`, which does not implement th
e `Copy` trait
308 |     b = B(a);
    |           - value moved here
309 |     // Explicitly dropping a breaches the ownership system.
310 |     drop(a); // Try to uncomment this line to see the error.
    |          ^ value used here after move
```

> Test: Can you summarize the behavior of `#[may_dangle]` in your own words?

## PhantomData in Drop Check

Everything seems perfect right now -- except only one issue left.
To see the subtle pitfall, let us write a Box-like struct ourselves.

```rust
fn phantom1() {
    struct MyBox<T>(*mut T); // T is not owned by MyVec because it's a pointer.
    unsafe impl<#[may_dangle] T> Drop for MyBox<T> {
        fn drop(&mut self) {
            println!("a dropped");
            unsafe {
                ptr::drop_in_place(self.0);
                alloc::dealloc(self.0 as *mut u8, Layout::new::<T>())
            };
        }
    }
    impl<T> MyBox<T> {
        fn new() -> MyBox<T> {
            MyBox(unsafe { alloc::alloc(Layout::new::<T>()) } as *mut T)
        }
        fn move_in(&mut self, mut t: T) {
            unsafe {
                ptr::swap(self.0, &mut t as *mut T);
            }
        }
    }

    let mut a = MyBox::new();
    let s = String::from("233");
    a.move_in(&s);
    drop(s);
    println!("s dropped");
    println!("&s dangles ever since");
    // a get dropped here when &s is dangling
}
```

```text
s dropped
&s dangles ever since
a dropped
```

If `T` is a reference type like the above example, `MyBox` can simply free all the
allocated space. We don't have to bother with dropping them since they are
borrowed instead of owned. That's why we are going to add `#[may_dangle]` for
the same reason as in the last chapter. `ptr::drop_in_place` would do nothing to
a reference. That meets our needs.


On the other hand, if `T` is actually OWNED by `MyBox` like `MyBox<T>`, we must
drop all of them individually. So we really need to have mutable access to them
and we hope our compiler check works in such cases. However, `#[may_dangle]`
loosens requirements for `T` and makes the hazardous code compile smoothly.

```rust
fn phantom2() {
    struct MyBox<T>(*mut T);
    struct PrintOnDrop<'s>(&'s str);
    impl<'s> Drop for PrintOnDrop<'s> {
        fn drop(&mut self) {
            println!("PrintOnDrop dropped as part of drop glue of MyBox");
            println!("visit a dangling reference: {}", self.0);
        }
    }
    unsafe impl<#[may_dangle] T> Drop for MyBox<T> {
    // If we use a safer variant, MyBox would take T into consideration. Why?
    // Remember the *last rule* in recursive drop check?
    // impl<T> Drop for MyBox<T> { 
        fn drop(&mut self) {
            println!("MyBox dropped");
            unsafe {
                ptr::drop_in_place(self.0);
                alloc::dealloc(self.0 as *mut u8, Layout::new::<T>())
            };
        }
    }
    impl<T> MyBox<T> {
        fn new() -> MyBox<T> {
            MyBox(unsafe { alloc::alloc(Layout::new::<T>()) } as *mut T)
        }
        fn move_in(&mut self, mut t: T) {
            unsafe {
                std::mem::forget(std::mem::replace(&mut *self.0, t));
            }
        }
    }

    let mut a = MyBox::new();
    let mut s = "Hello".to_owned();
    s.push_str(" world");
    a.move_in(PrintOnDrop(s.as_str()));
    drop(s);
    println!("s dropped");
    // MyBox dropped here
}
```

```
output
��
```
(jemalloc may give you the correct "Hello world" due to its optimization for
small memory allocation. But not for sure.)

The point to resolve this trouble is to make T owned by MyVec in some way.
Something tricky like a zero-sized array in C language might have it settled but
in rust we have a dedicated type, `PhantomData<T>`, for this. What is
[PhantomData](https://doc.rust-lang.org/std/marker/struct.PhantomData.html)?

```rust
fn phantom3() {
    struct MyBox<T>(*mut T, PhantomData<T>);
    struct PrintOnDrop<'s>(&'s str);
    impl<'s> Drop for PrintOnDrop<'s> {
        fn drop(&mut self) {
            println!("PrintOnDrop dropped as part of drop glue of MyBox");
            println!("visit a dangling reference: {}", self.0);
        }
    }
    unsafe impl<#[may_dangle] T> Drop for MyBox<T> {
        fn drop(&mut self) {
            println!("MyBox dropped");
            unsafe {
                ptr::drop_in_place(self.0);
                alloc::dealloc(self.0 as *mut u8, Layout::new::<T>())
            };
        }
    }
    impl<T> MyBox<T> {
        fn new() -> MyBox<T> {
            MyBox(
                unsafe { alloc::alloc(Layout::new::<T>()) } as *mut T,
                PhantomData::default(),
            )
        }
        fn move_in(&mut self, mut t: T) {
            unsafe {
                std::mem::forget(std::mem::replace(&mut *self.0, t));
            }
        }
    }

    let mut a = MyBox::new();
    let mut s = "Hello".to_owned();
    s.push_str(" world");
    a.move_in(PrintOnDrop(s.as_str()));
    drop(s);
    println!("s dropped");
}
```

```text
error[E0505]: cannot move out of `s` because it is borrowed
   --> src/main.rs:440:10
    |
437 |     let mut s = "Hello".to_owned();
    |         ----- binding `s` declared here
438 |     s.push_str(" world");
439 |     a.move_in(PrintOnDrop(s.as_str()));
    |                           - borrow of `s` occurs here
440 |     drop(s);
    |          ^ move out of `s` occurs here
441 |     println!("s dropped");
442 | }
    | - borrow might be used here, when `a` is dropped and runs the `Drop` code for type `phan
tom3::MyBox`
```

# Summary

The drop glue is responsible for removing all the allocated resources but the
strict drop order is sometimes unnecessary for a container type. We slacken the
generic checks by `#![may_dangle]`. It works most of the time. But in some
corner cases, the compiler is totally incapacitated from detecting use-after-free
issues. We ought to use `PhantomData` to apprize the compiler of the ownership
explicitly.
