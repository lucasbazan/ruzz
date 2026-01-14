<p align="center">
  <img src="assets/ruzz_logo.png" alt="Ruzz Logo">
</p>

A powerful fuzzing tool for web application testing.

## Installation

### By building from source
1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/ruzz.git
   cd ruzz
   ```
2. Build the project:
   ```bash
   cargo build --release
   ```
3. The compiled binary will be located in the `target/release` directory.
4. (Optional) Move the binary to a directory in your PATH for easier access:
   ```bash
   mv target/release/ruzz /usr/local/bin/
   ```


### Using precompiled binaries
1. Download the latest release from the [Releases](https://github.com/lucasbazan/ruzz/releases/latest) page.
2. Extract the downloaded archive.
3. Move the binary to a directory in your PATH for easier access:
   ```bash
   mv ruzz /usr/local/bin/
   ```

###

## Usage

### Basic Syntax

#### Linux
```bash
./ruzz [action options] [configuration options]
```

#### Windows
```bash
.\ruzz.exe [action options] [configuration options]
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
  Define wordlists for fuzzing in JSON format (used in SHUFFLE mode).:
  ```bash
  -wm "{'fuzz1':'path/to/wordlists/fuzz1.txt', 'fuzz2':'path/to/wordlists/fuzz2.txt'}"
  ```
- **`-w, --wordlist <file>`**  
  Path to a single wordlist file (used in MONO mode).
  ```bash
  -w "/path/to/wordlist.txt"
  ```

### Fuzzing Mode

- **`-m, --mode <mode>`**  
  Fuzzing mode (default: `shuffle`):
  - **`shuffle`**: Tests all possible combinations between wordlists
  - **`mono`**: Tests all the fuzz placeholders with the same wordlist simultaneously

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

- **`-rl, --rate-limit <rate>`**  
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
  -rl 50 \
  -H "Authorization: Bearer token" \
  -v debug
```

### Mono mode fuzzing

```bash
ruzz -t target.com/:FUZZ1:/:FUZZ2: \
  -w "/path/to/wordlist.txt" \
  -m mono \
  -ec 404
```

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Contributing

See the [CONTRIBUTING](CONTRIBUTING.md) guide for details on how to contribute to this project.

<p align="center">made with ❤️ by Lucas Bazan</p>