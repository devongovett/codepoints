# codepoints

A parser for files in the Unicode database. Produces a giant array of codepoint objects for
every character represented by Unicode, with many properties derived from files in the Unicode
database.

**BUILD SCRIPTS ONLY**: Use in production is not recommended
as the parsers are not optimized for speed, the text files are huge, and the resulting array uses a
huge amount of memory. To access this data in real world applications, use modules that have
precompiled the data into a compressed form:

* [unicode-properties](https://github.com/devongovett/unicode-properties)

## Installation

Install using npm:

    npm install codepoints

## Usage

Basic usage:

```js
codepoints = require('codepoints');
```

The parser generates data by reading the text files contained in the
[Unicode Character Database](http://unicode.org/ucd/). By default, it will use the database
bundled with this package. To use a custom version of UCD, use `codepoints/parser` instead,
which accepts an optional path to a directory containing the uncompressed UCD data:

```js
parser = require('codepoints/parser');
codepoints = parser('/path/to/UCD');
```

## Codepoint data

Each element in the generated array is either `undefined` (for unassigned code
points), or an object containing the following properties:

* `code` - the code point index
* `name` - character name
* `unicode1Name` - legacy name used by Unicode 1
* `category` - Unicode category
* `block` - the block name this character is a part of
* `script` - the script this character belongs to
* `eastAsianWidth` - the east asian width for this character
* `combiningClass` - numeric combining class value
* `combiningClassName` - a string name for the combining class
* `bidiClass` - class for the Unicode bidirectional algorithm
* `bidiMirrored` - whether the character is mirrored in the bidi algorithm
* `numeric` - the numeric value for this character
* `uppercase` - an array of code points mapping this character to upper case, if any
* `lowercase` - an array of code points mapping this character to lower case, if any
* `titlecase` - an array of code points mapping this character to title case, if any
* `folded` - an array of code points mapping this character to a folded equivalent, if any
* `caseConditions` - conditions used during case mapping for this character
* `decomposition` - an array of code points that this character decomposes into. Used by the Unicode normalization algorithm.
* `compositions` - a dictionary mapping of compositions for this character
* `isCompat` - whether the decomposition is a compatibility one
* `isExcluded` - whether the character is excluded from composition
* `NFC_QC` - quickcheck value for NFC (0 = YES, 1 = NO, 2 = MAYBE)
* `NFKC_QC` - quickcheck value for NFKC (0 = YES, 1 = NO, 2 = MAYBE)
* `NFD_QC` - quickcheck value for NFD (0 = YES, 1 = NO)
* `NFKD_QC` - quickcheck value for NFKD (0 = YES, 1 = NO)
* `joiningType` - arabic joining type
* `joiningGroup` - arabic joining group

## License

MIT
