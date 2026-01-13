<p align="center">
  <img src="assets/ruzz_logo.png" alt="Ruzz Logo">
</p>

A powerful fuzzing tool for web application testing.

## Installation

```bash
# TODO - Add installation instructions here
```

## Usage

### Basic Syntax

```bash
ruzz [action options] [configuration options]
```

## Action Options

### Target Configuration

- **`-tl, --targets-list <file>`**  
  Path to a file containing a list of targets. Fuzz placeholders must be enclosed in colons (e.g., `:FUZZ1:`, `:FUZZ2:`).  
  **Note:** Placeholders are case-sensitive.

- **`-t, --target <target>`**  
  Single target (can be a URL, domain, or IP address).

### Wordlist Mapping

- **`-wm, --wordlists-mapping <mapping>`**  
  Define wordlists for fuzzing using JSON format:
  ```bash
  -wm "{'fuzz1':'path/to/wordlists/fuzz1.txt', 'fuzz2':'path/to/wordlists/fuzz2.txt'}"
  ```

### Fuzzing Mode

- **`-m, --mode <mode>`**  
  Fuzzing mode (default: `shuffle`):
  - **`shuffle`**: Tests all possible combinations between wordlists
  - **`row`**: Tests line-by-line (first line of fuzz1 with first line of fuzz2, and so on)

### Response Filtering

- **`-ic, --include-code <codes>`**  
  Only include responses with specific status codes (comma-separated).  
  Example: `200,300,405`

- **`-ec, --exclude-code <codes>`**  
  Exclude responses with specific status codes (comma-separated).  
  Example: `404,414`

## Configuration Options

- **`-v, --verbose <level>`**  
  Set verbosity level: `info`, `debug`, or `error`

- **`-H, --header <header>`**  
  Add custom HTTP header

- **`-C, --cookie <cookie>`**  
  Add cookie to requests

- **`-x, --threads <number>`**  
  Number of concurrent threads

- **`-r, --rate-limit <rate>`**  
  Rate limit in requests per second

- **`-d, --delay <seconds>`**  
  Delay between each request

## Examples

### Using a targets list file

```bash
ruzz -tl path/to/target/list.txt -wm "{'FUZZ1':'wordlist1.txt', 'FUZZ2':'wordlist2.txt'}"
```

### Single target with fuzzing

```bash
ruzz -t google.com/:FUZZ1:/:FUZZ2: -wm "{'FUZZ1':'dirs.txt', 'FUZZ2':'files.txt'}"
```

### Advanced example with filters and configuration

```bash
ruzz -t example.com/api/:FUZZ1: \
  -wm "{'FUZZ1':'endpoints.txt'}" \
  -ic 200,201,301 \
  -x 10 \
  -r 50 \
  -H "Authorization: Bearer token" \
  -v debug
```

### Row mode fuzzing

```bash
ruzz -t target.com/:FUZZ1:/:FUZZ2: \
  -wm "{'FUZZ1':'users.txt', 'FUZZ2':'passwords.txt'}" \
  -m row \
  -ec 404
```

## License

TODO - [Add your license here]

## Contributing

TODO - [Add contribution guidelines here]