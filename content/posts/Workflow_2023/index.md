---
title: "My Paper-Reading Workflow in 2023"
date: 2023-09-01T23:37:13+08:00
draft: false
tags: ["productivity", "workflow"]
---

# Main

The conventional approach to storing a file involves fitting it into a
hierarchical structure that necessitates a comprehensive overview of the
corresponding field before the very first paper reading. You may place them
flattened in an inbox folder before the tedious task of reindexing and
categorizing hundreds of them hierarchically, otherwise, the overwhelming folder
becomes your first obstacle to retrieve information. However, it can be deduced
that both methods involve an additional burden of metal. Furthermore, the fact
that papers can be organized in multiple ways compounds the disaster in a
hierarchical system where one paper is only placed in one place. Therefore, an
ideal structure of notetaking of papers should be bottom-up, where papers are
connected like a web and a single paper can be attached to distinct categories.

Zotero is wonderful for personal usage for links in notes, cross-platform, and tags.
The free storage size of Zotero is only 300 MB. For computer vision papers with
many pictures, it's easy to have a PDF attachment larger than 10 MB so that only
30 papers can be stored. Fortunately, we can move all the attachments to another
directory using ZotFile and leave a link to the attachment. The attachment
directory can be synchronized to your cloud. Everything
works fine before it comes to a group. In a group library, you are not able to
create a link to your local file but a network link. I can provide a WebDAV
service on my server so that all large attachments are stored there. So that's
it.

My paper-reading workflow can be summarized as follows:
1. Find papers of interest
2. Import the paper into the local TOREAD collection in Zotero
3. Read it, take notes, add tags and relations
4. Move the paper item to a group collection and the pdf file together with
   notes to a WebDAV server
5. Create links to the pdf and notes on the WebDAV server

---

# Appendix

## Some useful addons in Zotero

[**ZotFile**](http://zotfile.com/) helps to manage your attachments
conveniently. This addon makes it possible to store attachments under a single
directory which is suitable for synchronization.

[**Better BibTex for
Zotero**](https://github.com/retorquere/zotero-better-bibtex) is designed to
enhance the ability of the BibTex generation. 

To give a broader view, let's first talk about what Zotero does. Zotero
*imports* meta information of items (e.g. papers, journals, books)
from various sources (e.g. webpages, arXiv IDs, pdf files) and store them in an
internal database so that you can *export* them in a variety of formats (e.g.
BibTex, Chicago-style citation, pandoc citation ). So the key point of
Zotero is just the quality of 

1. Extracting metainfo from diverse sources and
2. Exporting to diverse formats.

Many plugins aim to improve these two segments. In the original Zotero, for
example, it is possible to mess up when two files have the same citation keys
which are used to uniquely identify a bibliography in BibTex. Better BibTex
for Zotero fixes this and gives you more freedom to control the format of the
citation keys. Many other advantages are listed on its [official
website](https://retorque.re/zotero-better-bibtex/).

[**Mdnotes for Zotero**](https://argentinaos.com/zotero-mdnotes/) exports meta
information as a markdown file which is useful for integrating with
[Obsidian](https://obsidian.md/)

Other useful add-ons include [Zotero
tag](https://github.com/windingwind/zotero-tag), [zotero-citationcounts
](https://github.com/eschnett/zotero-citationcounts),
[zotero-better-notes](https://github.com/windingwind/zotero-better-notes)

## Other tools

I use [alist](https://alist.nn.ci/) as my WebDAV service provider and
[rclone](https://rclone.org/) to mount WebDAV. 

