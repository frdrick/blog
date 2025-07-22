---
layout: post
title: "Inserting special characters in Neovim - Digraphs"
date: 2025-07-22 19:56:45
categories: vim neovim unicode
---

I was trying to insert the character ë recently and had to resort to googling _Bronte_ and copying the ë from the results. I wondered if there was some easier way of doing this in the future and found out a post by jdhao: [inserting unicode characters in vim/neovim][jdhao] about digraphs.

In linguistics digraphs are used to represent a singular sound using a pair of characters. So, in neovim when it comes to characters like œ or æ which are typed quite intuitively whilst in **insert** mode:

- œ = `Ctrl-K oe`
- æ = `Ctrl-K ae`

This then follows for a range of other letters for instance:

- ë = `Ctrl-K e:`
- α = `Ctrl-K a*` (the same follows for other greek letters - though note latex can be funny rendering text with any unicode characters)

For more useful information on writing special characters in neovim see `:h digraphs`.
For a complete list of digraphs in (neo)vim please see `:digraphs`. Here they will also be converted to their code to be used with `Ctrl-V` in **insert** mode. For instance Ë = `Ctrl-V 203` so in the list in :digraphs we see:

- E: Ë 203

[jdhao]: https://jdhao.github.io/2020/10/07/nvim_insert_unicode_char/
