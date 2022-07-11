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

