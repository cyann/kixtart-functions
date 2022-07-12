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

## acronym($string)
Return the acronym of a string.

## base64_encode_native($string)
Convert a string to its Base64 equivalent (slow).

## base64_encode($string)
Return the Base64 conversion of the provided string (fast).

## cdbl_to_string($cdbl, optional $decimals)
Convert and round a double-precision floating-point value (cdbl) to a string with a dot (.) as numerical separator.

## dn_to_ou($dn)
Shorten an LDAP DN (Distinguished Name) to an OU name.

## to_ascii7($string, optional $replacement_char)
Normalize a string to 7-bit ASCII.

## url_encode($string)
Convert a string to be RFC 1738 compliant.

---

## Flag functions
Functions that deal with strings containing zero or more semicolon-separated flags. For example `flag1;flag2;flag3`.

## sort_list($list, optional $separator)
Return a sorted list of words separated by semicolon (;).

## add_flag($string, $flag)
 Add a flag to a semicolon separated string of flags.
function

## delete_flag($string, $flag)
Remove a flag from a semicolon separated string of flags.

---

# Array functions

## clean_up_array($array)
Clean up an array from commas and extra spaces.

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

## exp($number, $exponent)
Return a number raised to the power of exponent.

## hex_to_date_time($hex_string)
Convert a reversed int8 hexadecimal string to a date time string.

## hex_to_dec($hex)
Convert an hexadecimal string to decimal.

## int8_to_date_time($hex_string)
Convert an int8 hex string or date object to a date time string.

## serial_date($serial)
Return the number of days since day 1 of the specified date (yyyy-mm-dd) or vice-versa.

## unix_to_date_time($unix_time)
Return a date (yyyy-mm-dd) from a UNIX timestamp.

## wmi_utc_to_date_time($wmi_utc)
Return the adjusted WMI UTC date time to the local time.

---

# File functions

## compare_version($initial_version, $compared_version)
Compare 2 version numbers (x.x.x.x).

## get_file_sha256($file_name)
Return the SHA-256 hash of the specified file.

## get_file_version_64($file, optional $field)
Return the file version details on x64-redirected file.

## get_temp_file()
Return a random temp file name.

## get_version_int($exe_path)
Return an integer from a x.yy version, e.g. 4.67 -> 467.

## is_file_identical($file1, $file2)
Return 1 if 2 files are identical.

## wkix_exe_path()
Install, update, and return the path to the local wkix.exe.

---

# Registry functions

## enum_key_64($key, $index)
Enumerate the native value of a registry key on x64.

## read_value_64($key, $name)
Read the 64-bit value of a registry key.

## reg_export($reg_key, $reg_file)
Export a registry key to a Regedit 5 format file (UCS-2 LE BOM).

---

# Networking functions

## post_data($url, $data)
Post data to a web service.

## subnet_mask_to_prefix($subnet_mask)
Return the prefix (/x value) of a subnet mask.

