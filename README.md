# SSM Specification
## Overview
SSM is a lightweight markup language for simple configurations. It supports value assignments, groupings, and comments in a human-readable format similar to INI files, with a more straightforward syntax.
## 1. File Structure
An SSM file consists of:
- **Ungrouped Values**: Key-value pairs that are not grouped, written outside any `[group]` section.
- **Grouped Values**: Key-value pairs grouped under a `[group_name]` declaration.
- **Comments**: Text comments that begin with a `#`.
Example:
```ssm
# This is an ungrouped value
example_value = "Hello, SSM!"

[group_name]
key1 = 42
key2 = "A grouped string"
```
## 2. Basic Elements
### 2.1 Key-Value Assignment
- Assign values to keys using the syntax: `key = value`.  
- Keys are alphanumeric and can contain underscores (`_`), but no whitespace.  
- Values can be:
  - **Strings**: Enclosed in double quotes ("...").
  - **Integers**: A sequence of digits (1234).

Example:
```ssm
name = "Simple Structured Markup"
version = 1
```
### 2.2 Groups
- Groups are declared by enclosing a group name in square brackets (`[group_name]`).
- Group names are alphanumeric and can contain underscores (`_`).
- Values under a group apply to the current group until a new group is defined or the file ends.

Example:
```ssm
[group1]
setting1 = 100
setting2 = "Grouped text"

[group2]
count = 5
```
### 2.3 Comments
- Comments start with `#` and continue to the end of the line.
- Comments can appear:
  - On a line by themselves.
  - At the end of a key-value assignment.

Example:
```ssm
# This is a standalone comment
name = "SSM" # This is an inline comment
```

## 3. Data Types
- **String**: Text wrapped in double quotes. SSM allows any characters within double quotes, including numbers, which will be treated as strings.
  - Example: `title = "Hello, World!"`
- **Integer**: A sequence of digits representing a whole number, without quotes.
  - Example: `version = 2`
        
## 4. Rules and Constraints
1. **Key Syntax**:
  - Must start with a letter or underscore.
  - Only alphanumeric characters and underscores are allowed (no spaces).

2. **Group Syntax**:
  - Must start with a letter or underscore.
  - Enclosed in square brackets (`[group_name]`).
  - Group name must not contain spaces.

3. **Value Syntax**:
  - Integers are written directly without quotes (e.g., `number = 42`).
  - Strings are enclosed in double quotes (e.g., `text = "hello"`).
  - Mixing integers and strings in a single value requires quoting (e.g., `mixed = "123abc"`).

4. **Comment Syntax**:
  - Begins with `#` and can be placed on any line.
  - Inline comments must be preceded by at least one space.

5. **No Nesting**:
  - SSM does not support nested groups or complex data types like arrays or dictionaries.

6. **Line Breaks**:
  - Each key-value pair or group declaration must be on its own line.

## 5. Examples
#### Example 1: Basic File Structure
```ssm
# An ungrouped key-value pair
application_name = "MyApp"

[general]
version = 1
description = "This is a simple app."

[database]
host = "localhost"
port = 5432
```
#### Example 2: Mixed Value Types
```ssm
name = "Sample Config" # App name as a string
timeout = 30 # Timeout in seconds as an integer

[server]
ip = "192.168.1.1"
port = 8080

[logging]
log_level = "info"
max_file_size = 1048576
```
## 6. Parsing and Usage Notes
- **Parser Considerations**:
  - An SSM parser should recognize lines starting with `#` as comments.
  - Group declarations (e.g., `[group_name]`) indicate that all subsequent key-value pairs belong to that group until a new group or end of file.
  - Ungrouped values are interpreted as global or general configuration settings.
