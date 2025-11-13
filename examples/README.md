# Examples

Examples of using `pytoony` to convert between TOON and JSON formats.

## Quick Start

### Convert TOON → JSON

```
# Convert file
pytoony example.toon -o example.json

# Output to console
pytoony example.toon

# From stdin
cat example.toon | pytoony
```

### Convert JSON → TOON

```
# Convert file (auto-detect format)
pytoony example.json -o example.toon

# Explicit direction
pytoony example.json -o example.toon --to-toon

# From stdin
cat example.json | pytoony --to-toon

# With custom indentation
pytoony example.json -o example.toon --to-toon --indent 4
```

## Example Files

### `example.toon` and `example.json`

Basic example with simple key-value pairs, nested objects, tabular arrays, and simple arrays.

### `array-example.toon` and `array-example.json`

Examples of various array types:

*   Tabular arrays (token-efficient format)
*   Simple string arrays
*   Numeric arrays
*   Mixed-type arrays

## Practical Examples

### 1\. Convert TOON to JSON

```
pytoony example.toon -o output.json
```

### 2\. Convert JSON to TOON

```
pytoony example.json -o output.toon
```

### 3\. View result in console

```
# TOON → JSON
pytoony example.toon

# JSON → TOON
pytoony example.json --to-toon
```

### 4\. Use in pipelines

```
# Convert and pipe to another tool
pytoony example.toon | jq '.name'

# Convert from stdin
echo 'name: Test' | pytoony
```

### 5\. Round-trip conversion (verification)

```
# TOON → JSON → TOON
pytoony example.toon -o temp.json
pytoony temp.json -o back.toon --to-toon

# Compare original and result
diff example.toon back.toon
```

## Auto-detection

`pytoony` automatically detects the input file format:

*   If file starts with `{` or `[` → JSON
*   Otherwise → TOON

So you can simply:

```
pytoony input.json -o output.toon  # Automatically detects JSON
pytoony input.toon -o output.json  # Automatically detects TOON
```

## Useful Options

*   `-o, --output` - specify output file (otherwise outputs to stdout)
*   `--to-toon` - explicitly specify conversion to TOON
*   `--indent N` - specify indentation size for TOON (default: 2)

## Usage Examples

```
# Simple conversion
pytoony example.toon -o example.json

# With custom indentation
pytoony example.json -o example.toon --to-toon --indent 4

# Pipeline
cat data.toon | pytoony | python process.py

# Batch conversion
for file in *.toon; do
    pytoony "$file" -o "${file%.toon}.json"
done
```