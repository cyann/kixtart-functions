# kixtart-functions
Helper functions for the KiXtart scripting language.

## Requirements
- KiXtart 4.61 or later.

## Notes
- Line endings (EOL) are CRLF.

## Prelude
The main script should begin with these options to enforce good coding practices. The variable `$x` is used as a temporary variable to avoid displaying the values returned by setoption().

```kix
break on

$x = setoption("explicit", "on")
$x = setoption("novarsinstring", "on")
$x = setoption("nomacrosinstrings", "on")
```

---

# String conversion functions

## base64_encode($string)
Convert a string to its Base64 equivalent (fast).

## sort_list($list, optional $separator)
Sort a list.

## to_ascii7($string, optional $replacement_char)
Normalize a string to 7-bit ASCII.

