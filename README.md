# KiXtart Functions
Helper functions for the [KiXtart](http://www.kixtart.org/) scripting language.

## Requirements
- KiXtart 4.61 or later.

## Notes
- Line endings (EOL) are CRLF.
- Indentation is using tabs.
- VS Code users can add the [KiXtart language syntax highlighting](https://marketplace.visualstudio.com/items?itemName=cyann.kixtart) extension.

## Caching
Slow functions, typically those using the network or WMI, should have their results cached within if they are called multiple times.

All the functions in this repository have their caching mechanisms removed to make them more simple to understand.

Example to add a cache to a function:
```kix
function slow_function()
	global $_slow_function
	if not $_slow_function
		; Do the thing and assign it to $_slow_function.
	endif
	$slow_function = $_slow_function
endfunction
```

## Prelude
The main script should begin with these options to enforce good coding practices. The variable `$x` is used as a temporary variable to avoid displaying the values returned by `setoption()`.

```kix
break on

$x = setoption("explicit", "on")
$x = setoption("novarsinstring", "on")
$x = setoption("nomacrosinstrings", "on")
```

---

# String conversion functions

- **`acronym`**($string) _Return the acronym of a string._
- **`base64_encode_native`**($string) _Convert a string to its Base64 equivalent (slow)._
- **`base64_encode`**($string) _Return the Base64 conversion of the provided string (fast)._
- **`cdbl_to_string`**($cdbl, [$decimals]) _Convert and round a double-precision floating-point value (cdbl) to a string with a dot (.) as numerical separator._
- **`dn_to_ou`**($dn) _Shorten an LDAP DN (Distinguished Name) to an OU name._
- **`to_ascii7`**($string, [$replacement_char]) _Normalize a string to 7-bit ASCII._
- **`trim_dc`**($dc) _Shorten an Active Directory DC (Domain Component)._
- **`url_encode`**($string) _Convert a string to be RFC 1738 compliant._

---

## Flag functions
Functions that deal with strings containing zero or more semicolon-separated flags. For example `flag1;flag2;flag3`.

- **`sort_list`**($list, [$separator]) _Return a sorted list of words separated by semicolon (;)._
- **`add_flag`**($string, $flag) _Add a flag to a semicolon separated string of flags._
- **`delete_flag`**($string, $flag) _Remove a flag from a semicolon separated string of flags._

---

# Array functions

- **`clean_up_array`**($array) _Clean up an array from commas and extra spaces._

---

# Date and time functions
> Date and time formatting functions, using a format compatible with ISO 8601 and RFC 3339 (yyyy-mm-dd hh:mm:ss).
> Attention: Most of these are not taking timezones, leap seconds and other time-related quirks into account.

- **`date_time_to_unix`**($date_time) _Return a UNIX timestamp from a date time string (yyyy-mm-dd hh:mm:ss)._

- **`date_time`**([$yyyy_mm_dd]) _Return the current date and time (yyyy-mm-dd hh:mm:ss)._

- **`date()`** _Return the date only (yyyy-mm-dd)._

- **`exp`**($number, $exponent) _Return a number raised to the power of exponent._

- **`hex_to_date_time`**($hex_string)_Convert a reversed int8 hexadecimal string to a date time string._

- **`hex_to_dec`**($hex) _Convert an hexadecimal string to decimal._

- **`int8_to_date_time`**($hex_string) _Convert an int8 hex string or date object to a date time string._

- **`serial_date`**($serial) _Return the number of days since day 1 of the specified date (yyyy-mm-dd) or vice-versa._

- **`unix_to_date_time($unix_time)
Return a date (yyyy-mm-dd) from a UNIX timestamp.

- **`wmi_utc_to_date_time($wmi_utc)
Return the adjusted WMI UTC date time to the local time.

---

# File functions
- **`compare_version`**($initial_version, $compared_version) _Compare 2 version numbers (x.x.x.x)._
- **`get_file_sha256`**($file_name) _Return the SHA-256 hash of the specified file._
- **`get_file_version_64`**($file, optional $field) _Return the file version details on x64-redirected file._
- **`get_temp_file()`** _Return a random temp file name._
- **`get_version_int`**($exe_path) _Return an integer from a x.yy version, e.g. `4.67` -> `467`._
- **`is_file_identical`**($file1, $file2) _Return 1 if 2 files are identical._

- **`wkix_exe_path()`** _Install, update, and return the path to the local `wkix.exe`._

---

# Registry functions

- **`enum_key_64`**($key, $index) _Enumerate the native value of a registry key on x64._
- **`read_value_64`**($key, $name) _Read the 64-bit value of a registry key._
- **`reg_export`**($reg_key, $reg_file) _Export a registry key to a Regedit 5 format file (UCS-2 LE BOM)._

---

# Networking functions
Functions to send data to web services, and deal with ip addresses.

- **`post_data`**($url, $data) _Post data to a web service._
- **`subnet_mask_to_prefix`**($subnet_mask) _Return the prefix (/x value) of a subnet mask._

---

# Information gathering functions
These functions should help gathering data about software, hardware, user, and networking configurations.

## Computer information
- **`computer_name()`** _Return the computer name._

## User information
- **`remote_session()`** _Return 1 if running in Terminal Services/RDP._
