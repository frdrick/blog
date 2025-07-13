---
layout: post
title: "Detecting and and running SQL queries from a text editor and subqueries via treesitter"
date: 2025-01-28 11:37:00 +0000
categories: sql treesitter lua
---

Recently I have been finding it quite cumbersome to run SQL subqueries nested within a larger query without manually copying and pasting these subqueries into an instance of SQL in the terminal. Having learnt about treesitter recently, I realised it could be used to detect queries or subqueries. Once detected they could be copied, pasted and run in an SQL instance.

## Introducing Treesitter

Treesitter generates a tree describing code from scripts in a general way that can be used to select text elements without using loads of regular expressions. For example, the following query - and any other query can be translated into a more general tree by treesitter.

```sql
SELECT *
FROM interview
WHERE person_id =
(SELECT id
FROM person
WHERE address_street_name = 'Diversey Circle';
```

Is described by the following code:

```query
(program ; [0, 0] - [6, 0]
  (statement ; [0, 0] - [5, 45]
    (select ; [0, 0] - [0, 8]
      (keyword_select) ; [0, 0] - [0, 6]
      (select_expression ; [0, 7] - [0, 8]
        (term ; [0, 7] - [0, 8]
          value: (all_fields)))) ; [0, 7] - [0, 8]
    (from ; [1, 0] - [5, 45]
      (keyword_from) ; [1, 0] - [1, 4]
      (relation ; [1, 5] - [1, 14]
        (object_reference ; [1, 5] - [1, 14]
          name: (identifier))) ; [1, 5] - [1, 14]
      (where ; [2, 0] - [5, 45]
        (keyword_where) ; [2, 0] - [2, 5]
        predicate: (binary_expression ; [2, 6] - [5, 45]
          left: (field ; [2, 6] - [2, 15]
            name: (identifier)) ; [2, 6] - [2, 15]
          right: (subquery ; [3, 0] - [5, 45]
            (select ; [3, 1] - [3, 10]
              (keyword_select) ; [3, 1] - [3, 7]
              (select_expression ; [3, 8] - [3, 10]
                (term ; [3, 8] - [3, 10]
                  value: (field ; [3, 8] - [3, 10]
                    name: (identifier))))) ; [3, 8] - [3, 10]
            (from ; [4, 0] - [5, 45]
              (keyword_from) ; [4, 0] - [4, 4]
              (relation ; [4, 5] - [4, 11]
                (object_reference ; [4, 5] - [4, 11]
                  name: (identifier))) ; [4, 5] - [4, 11]
              (where ; [5, 0] - [5, 45]
                (keyword_where) ; [5, 0] - [5, 5]
                predicate: (binary_expression ; [5, 6] - [5, 45]
                  left: (field ; [5, 6] - [5, 25]
                    name: (identifier)) ; [5, 6] - [5, 25]
                  right: (literal)))))))))) ; [5, 28] - [5, 45]
```

## Setup

To have our SQL (sub)query detector to exclusively run in SQL files I configured this in `sql.lua` from the directory tree below. In this directory, `FILETYPE.lua` only runs when `FILETYPE` is opened.

```
.config/nvim/after/ftplugin
├── lua.lua
├── markdown.lua
├── python.lua
├── sh.lua
├── sql.lua
├── tex.lua
└── text.lua
```

Now we'll have a look in how we detect queries/subqueries in `sql.lua`

In `sql.lua` we start with the following:

```lua
-- access treesitter parser plugin
local parsers = require 'nvim-treesitter.parsers'
-- get parser for a given buffer
local parser = parsers.get_parse()
-- save the parsed current buffer as a tree
local tree = parser:parse()[1]
-- find the root of the tree (to ensure our loops don't last forever later)
local root = tree:root()
local root_type = root:type()
```

## Finding our node of interest

```lua

```

[if-coding-were-natural]: https://www.youtube.com/watch?v=IRd2zwF527M&t=1646s
