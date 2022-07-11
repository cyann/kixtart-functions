# KiXtart Functions
Helper functions for the [KiXtart](http://www.kixtart.org/) scripting language.

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
Return the Base64 conversion of the provided string (fast).

## sort_list($list, optional $separator)
Return a sorted list of words separated by semicolon (;).

## to_ascii7($string, optional $replacement_char)
Normalize a string to 7-bit ASCII.

## url_encode($string)
Convert a string to be RFC 1738 compliant.

---

# Date and time functions
> Date and time formatting functions, using a format compatible with ISO 8601 and RFC 3339 (yyyy-mm-dd hh:mm:ss).
> Attention: Most of these are not taking timezones, leap seconds and other time-related quirks into account.

# date_time_to_unix($date_time)
Return a UNIX timestamp from a date time string (yyyy-mm-dd hh:mm:ss).

## date_time()
Return the current date and time (yyyy-mm-dd hh:mm:ss).

## date()
Return the date only (yyyy-mm-dd).

## serial_date($serial)
Return the number of days since day 1 of the specified date (yyyy-mm-dd) or vice-versa.

## unix_to_date_time($unix_time)
Return a date (yyyy-mm-dd) from a UNIX timestamp.

## wmi_utc_to_date_time($wmi_utc)
Return the adjusted WMI UTC date time to the local time.

---

# File functions

## get_file_sha256($file_name)
Return the SHA-256 hash of the specified file.

## get_file_version_64($file, optional $field)
Return the file version details on x64-redirected file.

## get_version_int($exe_path)
Return an integer from a x.yy version, e.g. 4.67 -> 467.

---

# Registry functions

## enum_key_64($key, $index)
Enumerate the native value of a registry key on x64.

---

# Networking functions

## subnet_mask_to_prefix($subnet_mask)
Return the prefix (/x value) of a subnet mask.

