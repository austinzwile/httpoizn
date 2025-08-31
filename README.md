# httpoizn

httpoizn is a Python tool for detecting HTTP Host & Header Poisoning vulnerabilities. It works by injecting randomized canaries into common HTTP headers and analyzes responses for reflections or meaningful differences.

## ✨ Features

* Canary-based poisoning detection (host & IP canaries).
* Supports custom canaries (--canary, --ip-canary).
* Reflection analysis in both response body and headers.
* Baseline comparison to catch subtle changes.
* Simple CLI with Typer subcommands.
* Color-coded output for easy triage.*

## ⚡ Installation

Requires **Python 3.11+**.

Clone and install locally with pipx (recommended):

```sh
git clone https://github.com/yourusername/httpoizn.git
cd httpoizn
pipx install .
```

Or install in a virtualenv:

```sh
pip install .
```

---
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

---

## 🖥️ Example Output
```
[+] Using host canary: z9hvgimj
[+] Using IP canary: 177.63.225.63
[-] No poisoning with header Host
[-] No poisoning with header X-Host
[+] Potential poisoning detected with header X-Forwarded-For

[+] Summary of poisoned responses:
  Header: X-Forwarded-For
    - Canary reflected in RESPONSE BODY
```

---

## 📋 Options
```
Usage: httpoizn [OPTIONS] COMMAND [ARGS]...

Commands:
  run       Run httpoizn against a target URL
  version   Show version information

Options for `run`:
  -u, --url TEXT        Target URL [required]
  -c, --canary TEXT     Custom host canary (optional)
  -i, --ip-canary TEXT  Custom IP canary (optional)
```

---

## ⚠️ Disclaimer

This tool is provided for educational and testing purposes only.Do not use against systems you do not own or have explicit permission to test.
