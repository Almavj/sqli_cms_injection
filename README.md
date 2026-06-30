# CVE-2026-26980 — Ghost CMS SQL Injection PoC

A Go-based proof-of-concept tool for demonstrating and validating the Ghost CMS Content API SQL injection vulnerability described by CVE-2026-26980.

> This tool is intended for authorized security research and testing only.

## Overview

The PoC targets Ghost CMS instances affected by a Content API slug filter ordering vulnerability. It can:

- verify whether a target is vulnerable to SQL injection
- retrieve a Content API key when possible
- enumerate a slug anchor
- extract an administrator email address
- optionally extract the admin password hash and admin API secret
- validate whether a patched target is no longer vulnerable

## Affected Versions

- Affected versions: Ghost CMS 3.24.0 through 6.19.0
- Fixed version: Ghost CMS 6.19.1
- CVE: CVE-2026-26980
- CWE: CWE-89
- Advisory: GHSA-w52v-v783-gw97

## Requirements

- Go 1.26.4 or a compatible newer version
- Network access to the target Ghost CMS instance
- A target that is either vulnerable or intended for validation testing

## Clone and Build

```bash
git clone https://github.com/gagaltotal/CVE-2026-26980-Ghost-CMS-Api
cd CVE-2026-26980-Ghost-CMS-Api
go mod tidy
go build -o ghost-sqli ghost_sqli_cms.go
```

You can also run it directly without building:

```bash
go run ghost_sqli_cms.go
```

## Usage

```bash
./ghost-sqli --url http://target:2368
```

### Common Options

- `--url <URL>`: Target Ghost CMS URL (required)
- `--validate-fix`: Test that the target is no longer vulnerable
- `--extract-password`: Also extract the admin bcrypt hash
- `--extract-api-key`: Also extract the admin API secret
- `--content-key <KEY>`: Skip setup and use an existing Content API key
- `-v`, `--verbose`: Enable verbose/debug output
- `-h`, `--help`: Show help

### Example Commands

```bash
./ghost-sqli --url http://target:2368
./ghost-sqli --url http://target:2368 --extract-password --extract-api-key
./ghost-sqli --url http://target:2368 --validate-fix
./ghost-sqli --url http://target:2368 -v
```

## Project Structure

- `ghost_sqli_cms.go`: Main Go implementation of the exploit and CLI
- `ghost_sqli/`: Supporting assets or related resources
- `images/`: Screenshots or reference material
- `go.mod`: Go module definition

