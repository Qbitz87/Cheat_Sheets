## Command-Line Usage (SpiderFoot HX - Cloud, or self-hosted)

```bash
# Basic Scan Structure (replace 'sf.py' with 'spiderfoot' if installed system-wide)
python ./sf.py -s <TARGET> [options]

# Core Options
-s <TARGET>        # Target to scan (e.g., domain, IP, email, username).
-t <TYPE>          # Target type (e.g., INTERNET_NAME, IP_ADDRESS, EMAILADDR, USERNAME, PHONENUMBER, BITCOIN_ADDRESS). Auto-detected if omitted for simple types like domain/IP.
-m <mod1,mod2,...> # Specify modules to run (comma-separated). Default: all applicable.
-M                 # List all available modules.
-o <OUTPUT_FILTER> # Specify which data types to output (CSV/JSON/GEXF). E.g., EMAILADDR, PII, VULNERABILITY_CVE_CRITICAL
-F <TYPES>         # Data types to highlight as findings (comma-separated).
-l <IP:PORT>       # Start the web UI listener on IP:PORT (e.g., 127.0.0.1:5001).

# Output Control
# Output is primarily via the web UI or reports generated from it.
# Command line can output specific findings filtered by -o.
```

## Command-Line Examples

```bash
# Scan a domain using all applicable modules, start web UI
python ./sf.py -s example.com -l 127.0.0.1:5001

# Scan a domain, but only run DNS and web scraping modules
python ./sf.py -s example.com -m sfp_dns,sfp_spider

# Scan an email address, focusing on finding associated accounts
python ./sf.py -s user@example.com -t EMAILADDR -m sfp_accounts,sfp_haveibeenpwned

# List all modules
python ./sf.py -M
```

## Web Interface Concepts (Access via `-l` option)

- **New Scan:** Define target, select modules (by Use Case, Data Required, or individually), run the scan.
- **Scans:** View running and completed scans.
- **Browse Data:** Explore discovered data elements visually or in tables.
- **Correlations:** View relationships SpiderFoot automatically identified.
- **Settings:** Configure API keys (crucial for many modules!), manage modules.
- **Export:** Generate reports (CSV, JSON, GEXF) from scan results.

## Common Module Categories (Examples)

- DNS (`sfp_dns`, `sfp_sublist3r`, ...)
- WHOIS (`sfp_whois`)
- Web Scraping/Spidering (`sfp_spider`, `sfp_crt`, `sfp_dnsdumpster`, ...)
- Threat Intelligence (`sfp_alienvault`, `sfp_virustotal`, `sfp_shodan`, ...)
- Social Media (`sfp_accounts`, `sfp_linkedin`, ...) (Often require API keys)
- Dark Web (`sfp_ahmia`, `sfp_tor`, ...)
- Vulnerabilities (`sfp_vulners`, `sfp_exploitdb`, ...)
- Metadata (`sfp_filemeta`)
