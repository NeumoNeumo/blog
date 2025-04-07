---
title: "Potential Implementation of `PolynomialSumOfSquaresList`"
date: 2025-04-06T17:17:04+08:00
draft: false
---

How do we prove $x^2+2x+1 \geq 0$ by sum of squares(SOS)? Quite trivial $\text{LHS}
= (x+1)^2 \geq 0$

Then, how to prove this by SOS?

$$1024 x^{12} + 1024 x^{11} - 2304 x^{10} - 2304 x^9 + 1856 x^8 + 1856 x^7 - 672 x^6 -
688 x^5 + 96 x^4 + 120 x^3 + x^2 - 8 x + 21 > 0$$

Note that

$$
\begin{align*}
& 1024 x^{12} + 1024 x^{11} - 2304 x^{10} - 2304 x^9 + 1856 x^8 + 1856 x^7 - 672 x^6 -
688 x^5 + 96 x^4 + 120 x^3 + x^2 - 8 x + 21 \\
=& \frac{953178310898788044405634417898675810098347314821670074294737731307329417300202257499761536478657283822781507633364642416166327278492431062378651278370657928662612204203551165032096670314311671897547870594071651961090916102146117367523334512377797063623918959641854483477219062452053117354701873293279721322207383101430406097244237282245639156393092313795413669142611049 x^{12}}{855628317881711343628447665505529353642205279926550721248508119951156125518248969209845948736002719280414541370639384443936720924614544681187805334420694749567400421129263862969704529965010066154381893028055449128137526516108909143872797671529580790648030301664407011259998219690161313333579998909002703175128634549361882868091571588610793879524527809926169868860955417600} \\
& +\frac{20730892603614552086030236791584376390584458016906737607737484410976414001063114786504571319170688941259188382102808494189006085284963556422616888222898922617541385760899893376535242468971667371887252593392744651799829664240827458028060434738895363938051839773370848251341085723828176528969737296885610550104284856922624395816262451042617170959861753944569051610115364975096073666531052259740236406867828388007841283785939762576367433335933838418591322151049217429629270341561448035039752629166572755121441300348424582513530988930032979543430868119319256707428034767673 \left(x^6-\frac{537192259959723196414608024276178584105895770740349990419864409450146859446360918141274261404347215931631797055464128276914916157874933032752787127367563050763626059546908325367179084235774333657723622129680953103417722133971649513536014377636992875729296614390814113462253672326830450300193835 x^5}{573436804488876102142203069716235581838573141198680442118406207394949540289519077190803351051243463518468145511138665086473396444014968827035817391723483821802914447475306468210874522306578884970990388833275010785029852472999820007452095481245595738959406070890816673619069129251781055609514481}\right)^2}{6206525292964998561634089879171420703703077222813245725237731062283243057781605384272715894893115688039561739976314528141440276348710982794310284305563578483338134927900379708528960238116906764065435465250988664286812424413087069804415610909501395560804213981736329016091614450301007081812989768771400716805356955326219422447174363315272321570725848811409107568938852180691630516174689224926595786145141068421753037366221895943861317367364438368687862455344412538507280470763541217796022531535278362226193304037113002012436942592035108049513404198504622679784592044800} \\
& +\frac{89049395936672352040168549073731104935508445899958191436161862318618887575473347824917288559803543779125075800645083670230091642794205786249413530141184376511491703526443536337740075607815663586644005996838313922814771433710991249266480332814634194309626307993872905338940207675367318393363919505638197260130676409010048261104018415934500084622706963281661906523350259253983921638707587 \left(x^6+\frac{1250035259177316292055552469386970079830476326367794092844767479864825753282605141675706859648589867835412955837749840441264047429340506451409551822678359781540767273795999093416096481298696046487871220 x^5}{8622143587826850910117502112533330587731675813130997925666043593533539304265371562476845710341277127329332016845355859683327927946544194588985145498192793223955868643181370645313715205428657738385563819}-\frac{250068555521657649046677562622926995400361492206054337746046763604698328360725525321979519080245347110841949526008580342735436820548070105753437244690660363635344349057576996446918551957050730363661467736795517432 x^4}{247000887631547219650362262267498217114359645814025727199754456680281704352551452248260792050311392387975177735397802907626080272289713051779703241439169224797693110058833779475283650861940201841910326516809614621}\right)^2}{341822602918637684462759803331862949268521644937598626784273477398092190810659753651937927998386651744723163423943913812097353506749855595813602901610410889636152000488013806377115269602857144079515823849827076508204604117044432065154126771800620953408005355692583886319844446768050888556173228514949931617518643948118914444108098243115937619771018949965589413350297216046547214310400} \\
& +\frac{114110582938612998704158659404514255051669057393030752659470219065049417311463468557376015892172386233408723378189272123039495190457682922779027347858586303115779007600668186892567924675431960334050645546500616838293445049 \left(x^6+\frac{170372215743602129824191290442816200114290980759432737980698537578762149431655574586767607141481342217936642217045286295 x^5}{79198978232815290130528655478941018199689976888747889206980181686545761334890064169317612189500341634270976992383855892}-\frac{10203953103929899682581976196753751277654908019629863829295675407122586862724024696782342783750780067856543386194463907683978113 x^4}{13451588692120113302853290112643611602282673701089314990715540684831684684396619555438945669199900573439855658045046218504735514}-\frac{1156921360237789757302485482040694552188225079328629147544405729241765179914524617193983587603792399575398269867536010269771984801215 x^3}{579480989267842360973616884762574144214735300369226600485034777161864144519121973828754340483462516803215541892922546046965501207606}\right)^2}{1366111482246106172696369013109580206661129472861465130693169324770543975649855414453178742347115059279451705556403540118352861235205455721219880514785580582513596385591992213465538746668601219072613820297212205392956700}\\
& +\frac{855170648996299453282826318597469637692688774342377279122588090583182914361725138849041618786410014540391013069612470521 \left(x^6+\frac{208824848701751946066177483431560679149593637501714562853898328 x^5}{1622430576418306376968793749919537014833913740547776937187465121}-\frac{1102891048931550800774133577726231389446852281283462307407302195510467736 x^4}{551125008995526254989473607432028592184518611427649841031577162693270089}-\frac{61451711586630000225725826920536158859746855484781118310242171140952718523128 x^3}{593547856562956888467288338364108993067921931542293187544982814791584554100775}+\frac{232473948787618155607377486386406989276269768205862051739439363838088892436 x^2}{237921979767491444391645439166417035735774063213781213491056607955450278625}\right)^2}{1734819496159721395301097762699887999566121344999250931454978497836495899386698353810674840031645076695859122690108416}\\
& +\frac{152625114303613097562970499342414182175024924456131965 \left(x^6+\frac{28563189249509387706470170536420805 x^5}{9315046557962779041251696063459844}-\frac{6454490216193107995064656609442859126128240 x^4}{6064787888379130847288192308311499387086309}-\frac{16732721532793552664373217343255126836816 x^3}{3553024507622509278691554818253293871345}+\frac{2619886181080527170645281731667006 x^2}{10684687385267909341688179834740825}+\frac{879726740067337452506895818594 x}{518598620844921096038838025275}\right)^2}{2087473500409210051198263446146771163219546655799312} \\
& +\frac{79747153878767503695019075279803 \left(x^6+\frac{740175552623215917780704 x^5}{8159383732850597703519153}-\frac{334868393274810914740397696 x^4}{120845381198458989757409079}-\frac{1582860475816375677208 x^3}{7966887686614702087275}+\frac{19812948366188776778252 x^2}{9085183041159657600375}+\frac{1284036836607616 x}{15467432289695097}-\frac{2247064464063328}{5155810763231699}\right)^2}{721328386522315927536627776512} \\
\gt &0
\end{align*}
$$


![](assets/meme.png)

**What happened behind the scenes?**
**How does mathematica get a monster like that?**

# Background

This problem stems back from Hilbert's 17th problem which asks
> Can a positive definite rational function always be expressed as a sum of
> squares of finitely many rational functions?

The answer to the problem is yes and it was proved by Emil Artin in 1927 using
formally real fields. The question here is a bit different because we are
asking whether it can be expressed as a sum of squares of polynomials(instead of
rational functions). It is a pity that the answer is no for general cases.
Motzkin polynomial $M(x,y) = x^4 y ^2 + x^2 y^4 -3x^2y^2 + 1 $ is an
counterexample because

$(x^4 y ^2 + x^2 y^4 + 1)/3 \geq \sqrt[3]{x^4 y ^2  x^2 y^4  1}=x^2y^2$ but you
cannot write it as a sum of squares of polynomials(have it a try by undetermined
coefficients).

But we can prove that some useful conclusions hold for polynomials in one
variable with rational coefficients.

# Existence of Polynomial SOS for Semidefinite Univariate Polynomials

**Prop 1**. Positive semidefinite univariate polynomial $f(x)$ of degree $2n$ with
rational coefficients can always be expressed as a sum of squares of
polynomials.

**Proof**. According to the fundamental theorem of algebra, $f(x)$ can be
factored as

$$
f(x)=c\prod_i(x-r_i)^2\prod_j((x-a_j)^2 + b_j)
$$

where $c,r_i,a_j,b_j\in \mathbb{Q}$ and $c, b_j>0$. Note that a sum of squares
multiplied by a sum of squares is still a sum of
squares. $\quad \blacksquare$

**Prop 2**. A univariate polynomial $ f(x) $ of degree $ 2n $ is
nonnegative if and only if there exists a positive semidefinite \((n+1) \times
(n+1)\) matrix \( A \) such that \( u^T A u = f(x) \), where \( u = [1, x, x^2,
\cdots, x^n]^T \). That is, there exists a positive semidefinite \((n+1) \times
(n+1)\) matrix \( A \) satisfying

\[
\sum_{\substack{i+j=k+2\\i,j\geq1}} A_{ij} = a_k,
\]  

where \( k = 0, 1, \cdots, 2n \), and \( a_k \) denotes the coefficient of \( x^k \).

**Hint**: Use the last prop.

Similarly, it follows that

**Prop 3**. A univariate polynomial $ f(x) $ of degree $ 2n $ is
positive definite if and only if there exists a positive definite \((n+1) \times
(n+1)\) matrix \( A \) such that \( u^T A u = f(x) \), where \( u = [1, x, x^2,
\cdots, x^n]^T \). That is, there exists a positive definite \((n+1) \times
(n+1)\) matrix \( A \) satisfying

\[
\sum_{\substack{i+j=k+2\\i,j\geq1}} A_{ij} = a_k,
\]

where \( k = 0, 1, \cdots, 2n \), and \( a_k \) denotes the coefficient of \(
x^k \).


# Algorithm

## First Attempt

From Prop 2, we have converted the problem to the existence of a semidefinite
matrix $A$ satisfying some linear constraints. This can be translated to a
semidefinite programming problem. The goal is zero since we only care about
the feasible set.

$$
\begin{align}
\text{Minimize}\quad& 0, \\
\text{s.t.} \quad &\sum_{\substack{i+j=k+2\\i,j\geq1}} A_{ij} =a_k,\\
& A\succeq 0
\end{align}
$$

But it is also reasonable to use $tr(A)$ as the objective function preventing
the entries of $A$ from being too large.

$$
\begin{align}
\text{Minimize}\quad& \text{tr}(A), \\
\text{s.t.} \quad &\sum_{\substack{i+j=k+2\\i,j\geq1}} A_{ij} =a_k,\\
& A\succeq 0
\end{align}
$$

There are a lot of methods to solve this semidefinite optimization problem. Only
the simplest one is demonstrated here. Making $A = B^T B$ ensures $A\succeq 0$.
Then minimize the following relaxed objective using gradient descent

$$
\mu\sum B_{ij}^2 + \sum_k(\sum_{\substack{i+j=k+2\\i,j\geq1}} A_{ij} -a_k)^2
$$

where the first term $\mu\sum B_{ij}^2 $ is a regularization initially set to 
$μ =0$ and gradually increased to promote small entries in $B$.

Then we get a numerical matrix $A$. Rationalize all the entries of $A$ with
sufficient accuracy. (You may want to try continued fractions to achieve the
best rational approximation with as small numerators and denominators as
possible.)

At this moment, $\sum_k(\sum_{\substack{i+j=k+2\\i,j\geq1}} A_{ij} -a_k)^2$ is a
small number but is not necessarily $0$. But we can expect $A$ is still
semidefinite after nudging some elements a little bit in $A$ to satisfy the
linear constraints. (A loophole here. We will fix it in the next subsection.) At
present, $A$ is a semidefinite matrix with rational entries and satisfies those
linear constraints. Let $A=CC^T$ be the Cholesky decomposition where $C$ is a
lower triangular matrix. Then the entries in $C^T u$ give the terms for
polynomial SOS. But $C$ is not necessarily a rational matrix.

It only leaves to prove that every column of $C$ is in the same quadratic field,
that is, for any $k=1,2,\cdots,n+1$, there exists $p_k\in\mathbb{N}_+$ such that
$C_{1k},C_{2k}, \cdots,C_{n+1,k}\in \mathbb{Z} [\sqrt{p_k}]$. If this holds, the
SOS can be written as 

$$
\sum_{i=1}^{n+1} p_k\left(\sum_{j=1}^{n+1}\frac{C_{ji}}{\sqrt{p_i}}x^{j-1}\right)^2
$$

Every coefficient in it is rational.

So let's prove this. Well, it is quite obvious from the following example, right?

$$
\begin{align*}
A & = CC^T = \begin{pmatrix}
C_{11} & 0 & 0 \\
C_{21} & C_{22} & 0 \\
C_{31} & C_{32} & C_{33}
\end{pmatrix} \begin{pmatrix}
C_{11} & C_{21} & C_{31} \\
0 & C_{22} & C_{32} \\
0 & 0 & C_{33}
\end{pmatrix} \\
&= \begin{pmatrix}
C_{11}^2 & \text{(symmetric)} \\
C_{21}C_{11} & C_{21}^2 + C_{22}^2 \\
C_{31}C_{11} & C_{31}C_{21} + C_{32}C_{22} & C_{31}^2 + C_{32}^2 + C_{33}^2
\end{pmatrix}
\end{align*}
$$

## Second Attempt

Remember the loophole in the last subsection? Nudging entries of a
positive semidefinite can possibly make the matrix non-positive semidefinite
because strictly semidefiniteness is a property *on the boundary* -- a little
distribution shall make the eigenvalue of the matrix change from 0 to a
negative value. Our method in the last subsection may fail when the input
polynomial is $x^2-2x+1$. What makes it worse is, numerical
calculation has trouble finding $(x-1)^2$ as the SOS for $x^2 - 2x + 1$ because
the feasible solution $A$ has to be precisely
$ \begin{pmatrix}
1 & -1 \\
-1 & 1
\end{pmatrix} $
which is quite impossible
for a floating point type in programming. (e.g. 0.1 + 0.2 != 0.3 in cpp)

All in all, we prefer positive definiteness over positive semidefiniteness in
computational optimization. Fortunately, the following prop helps us wipe
out semidefinite situations.

**Prop 4**. If $f(x)\in\mathbb{Q}[x]$ is a positive semidefinite polynomial, then
$f(x)$ can be factored as $g^2(x)h(x)$ where $g,h\in\mathbb{Q}
[x]$ and $h(x)$ is positive definite.

**Proof**. We'll prove it by induction for the degree $2n$ of $f(x)$. If $n=0$,
it is trivial. If we have proved the prop for $n=k-1$, let's prove it for $n=k$.
If $f(x)$ has no real root, it must be positive definite, the prop proved. If
$f(x)$ has real root $\alpha$, the multiplicity of $\alpha$ must be an even
number $2t$. Denote the minimal polynomial of $\alpha$ as $p(x)$. Suppose $f(x)
= p^m(x)q(x)$ where $p \nmid q$. It is apparent $m \leq 2t$. 

If $m\lt 2t$, 
the $m$th derivative of $f(x)$ has a root of $\alpha$ since the multiplicity is
$2t-1\geq m$. On the other hand,

$$
f^{(m)}(x) = \sum_{k=0}^{m} \binom{m}{k} [p^m(x)]^{(k)} \cdot q^{(m-k)}(x)
$$

among which the terms for $k=0,1,\cdots,m-1$ have a factor of $p(x)$. Thus,
$0 = f^{(m)}(\alpha) = m![p'(\alpha)]^mq(\alpha)$ while $p\nmid m![p']^mq$,
leading to a contradiction. Therefore $m=2t$. 

$f(x)/p^{2t}(x)$ is positive semidefinite. Thus $f(x)/p^{2t}(x)$ can be
expressed as $u^2 v$ where $u,v\in\mathbb{Q}[x]$ and $v$ is positive definite.
The proof is finished by $f = (p^t u)^2 v$. $\quad \blacksquare$.

In algorithm, we can first decomposite the function $f(x)$ in $\mathbb{Q}[x]$ to
get $p$ and $q$(check [this wiki page](https:
//en.wikipedia.org/wiki/Factorization_of_polynomials) for more methods). Then
find the polynomial SOS for $q$. Finally, combine $p,q$ together.

## Final Algorithm

(Modified from text generated by Deepseek)

**Input**:  
A polynomial \( f(x) \in \mathbb{Q}[x] \) that is **positive semidefinite** (i.e., \( f(x) \geq 0 \) for all \( x \in \mathbb{R} \)).

**Output**:  
A rational sum-of-squares (SOS) decomposition of \( f(x) \), expressed as:  
\[
f(x) = \sum_{i} p_i \left( g_i(x) \right)^2,
\]  
where \( g_i(x) \in \mathbb{Q}[x] \) and \( p_i \in \mathbb{Q}_+ \).


**Steps**:

1. **Factorization Step** (Prop 4):  
   - Factor \( f(x) \) as \( f(x) = g^2(x) h(x) \), where:  
     - \( g(x) \in \mathbb{Q}[x] \) captures **all repeated roots** (if any),  
     - \( h(x) \in \mathbb{Q}[x] \) is **positive definite** (i.e., \( h(x) > 0 \) for all \( x \in \mathbb{R} \)).  
   - **Method**:  
     - Compute the square-free factorization of \( f(x) \) (e.g., using Yun’s algorithm).  
     - Extract \( g(x) \) as the product of all repeated irreducible factors (with even exponents).  
     - The remaining part \( h(x) = f(x)/g^2(x) \) will have no repeated roots and be positive definite.

2. **Semidefinite Programming (SDP) for \( h(x) \)** (First Attempt):  
   - Represent \( h(x) \) in the basis \( \{1, x, x^2, \dots, x^n\} \).  
   - Formulate the SDP problem:  

     \[
     \begin{align*}
     \text{Minimize} \quad & \text{tr}(A), \\
     \text{s.t.} \quad & \sum_{\substack{i+j=k+2 \\ i,j \geq 1}} A_{ij} = a_k \quad \text{(coefficient matching)}, \\
     & A \succeq 0 \quad \text{(positive semidefinite constraint)}.
     \end{align*}
     \]  

   - **Relaxed Optimization**:  
     - Parameterize \( A = B^T B \) to ensure \( A \succeq 0 \).  
     - Solve using gradient descent on the relaxed objective:  

       \[
       \mu \sum B_{ij}^2 + \sum_k \left( \sum_{\substack{i+j=k+2 \\ i,j \geq 1}} A_{ij} - a_k \right)^2,
       \]  

       where \( \mu \) is gradually increased to regularize \( B \).  
     - Rationalize the entries of \( A \) (e.g., using continued fractions).
     - Nudge the entries to satisfy the linear constraints of constraint
       matching.

3. **Cholesky Decomposition**:  
   - Compute the Cholesky decomposition \( A = CC^T \), where \( C \) is lower triangular.  
   - **Key Insight**: Each column of \( C \) lies in a quadratic field \( \mathbb{Q}[\sqrt{p_k}] \).  
   - Construct the SOS terms:  

     \[
     h(x) = \sum_{k=1}^{n+1} p_k \left( \sum_{j=1}^{n+1} \frac{C_{jk}}{\sqrt{p_k}} x^{j-1} \right)^2.
     \]  

     All coefficients are rational.

4. **Combine Results**:  
   - Multiply back by \( g^2(x) \) to obtain the final SOS decomposition for \( f(x) \):  

     \[
     f(x) = g^2(x) \sum_{k} p_k \left( g_k(x) \right)^2.
     \]  


# Appendix

The code to generate the monstrous formula in mathematica at the beginning is as
follows.
```mathematica
f[x_] := 
  1024 x^12 + 1024 x^11 - 2304 x^10 - 2304 x^9 + 1856 x^8 + 
   1856 x^7 - 672 x^6 - 688 x^5 + 96 x^4 + 120 x^3 + x^2 - 8 x + 21;
makeMonicAndExtractLC[polys_List, var_] := 
 Module[{lcList, monicPolys}, 
  lcList = Coefficient[#, var, Exponent[#, var]] & /@ polys;
  monicPolys = MapThread[#1/#2 &, {polys, lcList}];
  {monicPolys, lcList}]
{monicPolys, lcList} = 
  makeMonicAndExtractLC[PolynomialSumOfSquaresList[f[x], x], x];
lcList^2*(monicPolys // Expand)^2 // Total
```

The minimum of this polynomial is very close to zero.
It is about $0.000506148$ when $x \approx 0.936309$

