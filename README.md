# httpoizn

httpoizn is a Python tool for detecting HTTP Host & Header Poisoning vulnerabilities. It works by injecting randomized canaries into common HTTP headers and analyzes responses for reflections or meaningful differences.

## ✨ Features

* Canary-based poisoning detection (host & IP canaries).
* Supports custom canaries (--canary, --ip-canary).
* Reflection analysis in both response body and headers.
* Baseline comparison to catch subtle changes.
* Simple CLI with Typer subcommands.
* Color-coded output for easy triage.

## ⚡ Installation

Requires **Python 3.11+**.

Clone and install locally with pipx (recommended):

```sh
❯ pipx install .
  installed package httpoizn 1.1.0, installed using Python 3.12.10
  These apps are now globally available
    - httpoizn
done! ✨
```

## 🔧 Usage

```sh
httpoizn run -u <url>
```

Examples:

```sh
httpoizn run -u https://target.com               # Run with random canaries
httpoizn run -u https://target.com -c mycanary   # Specify custom host canary
httpoizn run -u https://target.com -i 6.6.6.6    # Specify custom IP canary
httpoizn version                                 # Show version
```

## 🖥️ Example Output
```
[+] Using host canary: z9hvgimj
[+] Using IP canary: 177.63.225.63
[-] No poisoning with header Host
[-] No poisoning with header X-Host
[+] Potential poisoning detected with header X-Forwarded-For
...
[+] Summary of poisoned responses:
  Header: X-Forwarded-For
    - Canary reflected in RESPONSE BODY
```

## 📋 Options
```
❯ httpoizn run --help

 Usage: httpoizn run [OPTIONS]

╭─ Options ─────────────────────────────────────────────────────────────────────────────────────╮
│ *  --url        -u      TEXT  Target URL [required]                                           │
│    --canary     -c      TEXT  Custom host canary string (optional)                            │
│    --ip-canary  -i      TEXT  Custom IP canary (optional)                                     │
│    --help                     Show this message and exit.                                     │
╰───────────────────────────────────────────────────────────────────────────────────────────────╯
```

## ⚠️ Disclaimer

This tool is provided for educational and testing purposes only.Do not use against systems you do not own or have explicit permission to test.
