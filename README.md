# Fuzzy

Fuzzy matching for [Meadow](https://github.com/mcdearman/meadow): finding the
texts a few typed letters mean, the likeliest first, and where in each the
letters fell. It is what a picker ranks its list with.

```meadow
use Fuzzy (rank, found, score, places)

rank "vlen" (\d -> d) ["Vector.length", "valueOf", "String.length"]
-- [("Vector.length", Found …), ("String.length", …)]: best first

found "gt" "getText"      -- Just (Found … [0, 3]): the g, and the T of Text
found "ba" "abc"          -- None: the letters are not there in order
```

A query matches a text when its letters are in the text in order, with
anything between them. Of all the ways they can be found, the one reported
scores highest:

- a letter at the start of a word counts for more: the first letter of the
  text, one after punctuation or a space, a capital after a small letter;
- letters next to each other count for more than the same letters apart, and
  each character skipped between two costs a little.

A query with spaces in it is several words: each has to be in the text,
anywhere, and the score is their sum. A small letter in the query matches
either case; a capital matches only a capital.

`rank query text items` answers the items the query is found in, best first;
of two found as well, the one with the shorter text, then the one that came
first. `places` are character indices into the text, in order: what to
highlight.

## Install

```sh
meadow add mcdearman/Fuzzy
```

## Licence

BSD 3-Clause: see [LICENSE](LICENSE).
