# KiXtart Functions
Helper functions for the [KiXtart](http://www.kixtart.org/) scripting language.

## Requirements
- KiXtart 4.61 or later.

## Notes
- Line endings (EOL) are CRLF.
- Indentation is using tabs, writing style is snake_case.
- VS Code users can add the [KiXtart language syntax highlighting](https://marketplace.visualstudio.com/items?itemName=cyann.kixtart) extension.
- GitHub does not have a syntax highlighter for KiXtart, you can use `autoit` as a replacement for code blocks. You could also add KiXtart to [github/linguist](https://github.com/github/linguist/blob/master/CONTRIBUTING.md) with the help of [kixtart-vs-code/syntaxes/kixtart.tmLanguage](https://github.com/cyann/kixtart-vs-code/blob/main/syntaxes/kixtart.tmLanguage).
- List functions return a string of values separated by semicolons.
- Active Directory OU functions return stripped strings, for example:
	- Full path: `\\domain.example.com\OU name\computer name`
	- Stripped result: `domain\OU name\computer name`
- Most of the functions below are designed to return a string.


## Prelude
The main script should begin with these options to enforce good coding practices. The variable `$x` is used as a temporary variable to avoid displaying the values returned by `setoption()`.

```autoit
break on

$x = setoption("explicit", "on")
$x = setoption("novarsinstring", "on")
$x = setoption("nomacrosinstrings", "on")
```

## Caching
Slow functions, typically those using network or WMI calls, should have their results cached within, even more so when they are called multiple times.

Most of the functions in this repository have their caching mechanisms removed to make them simpler to understand, a notable exception being `ip_info()`.

Example to add a cache to a function:
```autoit
function slow_function()
	global $_slow_function
	if not $_slow_function
		; Do the thing and assign it to $_slow_function.
	endif
	$slow_function = $_slow_function
endfunction
```


---

# Core functions
These functions are required by other functions.

## String conversion functions
- **`acronym(`**`$string`**`)`** _Return the acronym of a string._
- **`base64_encode_native(`**`$string`**`)`** _Convert a string to its Base64 equivalent (slow)._
- **`base64_encode(`**`$string`**`)`** _Return the Base64 conversion of the provided string (fast)._
- **`browser_name(`**`$browser_path`**`)`** _Return the product name of the browser based on it's path._
- **`cdbl_to_string(`**`$cdbl, [$decimals]`**`)`** _Convert and round a double-precision floating-point value (cdbl) to a string with a dot (.) as numerical separator._
- **`cipher_to_hex(`**`$cipher`**`)`** _Convert a cipher suites to its hex code._
- **`dn_to_ou(`**`$dn`**`)`** _Shorten an LDAP DN (Distinguished Name) to an OU name._
- **`to_ascii7(`**`$string, [$replacement_char]`**`)`** _Normalize a string to 7-bit ASCII._
- **`trim_dc(`**`$dc`**`)`** _Shorten an Active Directory DC (Domain Component)._
- **`url_encode(`**`$string`**`)`** _Convert a string to be RFC 1738 compliant._


## Flag functions
Functions that deal with strings containing zero or more semicolon-separated flags. For example `flag1;flag2;flag3`.
- **`add_flag(`**`$string, $flag`**`)`** _Add a flag to a semicolon separated string of flags._
- **`delete_flag(`**`$string, $flag`**`)`** _Remove a flag from a semicolon separated string of flags._
- **`sort_list(`**`$list, [$separator]`**`)`** _Return a sorted list of words separated by semicolon (;)._


## Array functions
- **`clean_up_array(`**`$array`**`)`** _Clean up an array from commas and extra spaces._


## Date and time functions
> These date and time formatting functions are design to use a format compatible with ISO 8601 and RFC 3339:
>
> `yyyy-mm-dd hh:mm:ss`
>
> Attention: Most of these are not taking timezones, leap seconds and other time-related quirks into account.
- **`date_time_to_unix(`**`$date_time`**`)`** _Return a UNIX timestamp from a date_time string._
- **`date_time()`** _Return the current date and time._
- **`date(`**`[$yyyy_mm_dd]`**`)`** _Return the date only._
- **`exp(`**`$number, $exponent`**`)`** _Return a number raised to the power of exponent._
- **`hex_to_date_time(`**`$hex_string`**`)`** _Convert a reversed int8 hexadecimal string to a date time string._
- **`hex_to_dec(`**`$hex`**`)`** _Convert an hexadecimal string to decimal._
- **`int8_to_date_time(`**`$hex_string`**`)`** _Convert an int8 hex string or date object to a date time string._
- **`serial_date(`**`$serial`**`)`** _Return the number of days since day 1 of the specified date or vice-versa._
- **`unix_to_date_time(`**`$unix_time`**`)`** _Return a date from a UNIX timestamp._
- **`wmi_utc_to_date_time(`**`$wmi_utc`**`)`** _Return the adjusted WMI UTC date time to the local time._


## File functions
- **`get_file_sha256(`**`$file_name`**`)`** _Return the SHA-256 hash of the specified file._
- **`get_file_version_64(`**`$file, [$field]`**`)`** _Return the file version details on x64-redirected file._
- **`get_temp_file()`** _Return a random temp file name._
- **`get_version_int(`**`$exe_path`**`)`** _Return an integer from a x.yy version, e.g. `4.67` -> `467`._
- **`is_file_identical(`**`$file1, $file2`**`)`** _Return 1 if 2 files are identical._
- **`wkix_exe_path()`** _Install, update, and return the path to the local `wkix.exe`._


## Registry functions
- **`enum_key_64(`**`$key, $index`**`)`** _Enumerate the native value of a registry key on x64._
- **`read_value_64(`**`$key, $name`**`)`** _Read the 64-bit value of a registry key._
- **`reg_export(`**`$reg_key, $reg_file`**`)`** _Export a registry key to a Regedit 5 format file (UCS-2 LE BOM)._


## Version functions
- **`compare_version(`**`$initial_version, $compared_version`**`)`** _Compare 2 version numbers (x.x.x.x)._
- **`version_latest(`**`$version_list`**`)`** _Return the latest version from a list._
- **`version_oldest(`**`$version_list`**`)`** _Return the oldest version from a list._


## Networking functions
Functions to send data to web services, and deal with ip addresses.

- **`ip_to_subnet(`**`$ip_address, $subnet_mask`**`)`** _Return the subnet of an IP and it's subnet mask._
- **`post_data(`**`$url, $data`**`)`** _Post data to a web service._
- **`subnet_mask_to_prefix(`**`$subnet_mask`**`)`** _Return the prefix (`/x` value) of a subnet mask._


---


# Information gathering functions
These functions should help gathering data about software, hardware, user, and networking configurations.

## Computer information
- **`computer_name()`** _Computer name._
- **`cpu_count()`** _Number of logical CPUs._
- **`cpu_speed_ghz()`** _CPU speed, in GHz._
- **`device_type()`** _Computer type [Desktop\Laptop|Server]._
- **`drive_free_gb()`** _Available free space on the system drive, in GB._
- **`drive_size_gb()`** _System drive size, in GB._
- **`ram_size_gb()`** _RAM size, rounded in GB (e.g. `3.75` -> `4.0`)._
- **`serial_number()`** _Serial number._
- **`shared_folder_list()`** _List of shared folders with their permissions._
- **`virtual_machine()`** _Acronym of the host VM product._


## Windows information
- **`is_legacy_windows()`** _Return 1 if running on a legacy version of Windows._
- **`windows_architecture()`** _Architecture supported by Windows [x86|x64]._
- **`windows_edition()`** _Windows edition ID, abbreviated._
- **`windows_install_date()`** _Windows installation or upgrade date._
- **`windows_language()`** _Windows system language._
- **`windows_product_suite()`** _Windows Product Suite number._
- **`windows_service_pack()`** _Windows service pack number._
- **`windows_version()`** _Version of Windows, including Embedded (e) and Server Core (c), for example `2012R2c`._


## Software information
- **`av_product()`** _Anti-virus product name (acronym like SEP)._
- **`av_scan_date()`** _Anti-virus last scan date (yyyy-mm-dd)._
- **`dotnet_version_list()`** _List of Microsoft .NET Framework versions._
- **`ie_version()`** _Internet Explorer version._
- **`office_version_list()`** _List of Microsoft Office versions._


## User information
- **`remote_session()`** _Return 1 if running in Terminal Services/RDP._
- **`user_browser_path()`** _Path to the user's default browser._
- **`user_language()`** _User selected language._
- **`user_proxy_mode()`** _Configuration mode of the user proxy._
- **`user_screensaver_timeout()`** _Screen saver timeout in minutes._
- **`user_screensaver()`** _User selected screen saver._


## Active Directory information
- **`domain_controller()`** _Name of the domain controller._
- **`enum_group_members(`**`$computer_or_domain, $group, [$filter]`**`)`** _Array of a computer or domain group's members._
- **`ip_subnet_location(`**`[$ip_subnet]`**`)`** _Active Directory subnet location._
- **`is_admin()`** _Return 1 if running as admin or system._
- **`site_name()`** _Active Directory site name._
- **`user_domain()`** _Active Directory user domain._
- **`user_id()`** _Active Directory user ID._
- **`user_name()`** _Full name of the user._
- **`user_ou()`** _Active Directory user OU._
- **`user_privileges()`** _Effective user's privileges based on AD group membership._
- **`user_rid()`** _Active Dirstory user relative identifier._


## Networking information
- **`ip_info(`**`$type`**`)`** _Information about the active network adapter: `[ip_address|mac_address|subnet_mask|default_gateway|mac_address_list]`._
- **`mac_address_list()`** _List of MAC addresses._
- **`mac_address()`** _Active MAC address._


## Misc. information
- **`invocation_type()`** _Script invocation type._


---


# Abbreviations and acronyms
- **DC**: Active Directory / LDAP **Domain Component**
- **DN**: Active Directory / LDAP **Distinguished Name**, usually looking like `CN=computer,OU=sub-ou,OU=ou,DC=sub-domain,DC=domain-root,DC=com`
- **GB**: Gigabyte, but these functions return results in gibibyte (GiB), 1 GiB = 1073741824 bytes
- **GHz**: Gigahertz
- **IE**: Internet Explorer
- **OS**: Operating System, usually Windows
- **OU**: Active Directory / LDAP **Organizational Unit**
- **WMI**: Windows Management Instrumentation
