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

---

# Date and time functions
> Date and time formatting functions, using a format compatible with ISO 8601 and RFC 3339 (yyyy-mm-dd hh:mm:ss).

## date_time()
Return the date and time (yyyy-mm-dd hh:mm:ss).

## date()
Return the date only (yyyy-mm-dd).

## serial_date($serial)
Convert a date (yyyy/mm/dd or yyyy-mm-dd) to the number of days since day 1 or vice-versa.

## wmi_utc_to_date_time($wmi_utc)
Adjust a WMI UTC time to the local time.

