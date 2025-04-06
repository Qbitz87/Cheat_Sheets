## Core Search Operators

```
"search phrase"        # Exact phrase search. Crucial for names, specific errors, etc.
		             # Example: "Ola Nordmann"

site:domain.com        # Restrict results to a specific website or domain.
                     # Example: site:regjeringen.no

filetype:xyz           # Search for specific file types (pdf, docx, xlsx, txt, log, etc.).
                     # Example: filetype:pdf

inurl:term             # Find pages with 'term' anywhere in the URL.
                     # Example: inurl:login

intitle:term           # Find pages with 'term' in the HTML title.
                     # Example: intitle:"index of"

intext:term            # Find pages with 'term' in the body text. Less precise but useful.
                     # Example: intext:"confidential report"

-term                  # Exclude results containing 'term'.
                     # Example: "internal report" -jobs

* # Wildcard for one or more words within a phrase.
                     # Example: "contact * information"

| or OR                # Logical OR (OR must be uppercase).
                     # Example: filetype:xls | filetype:xlsx   OR   filetype:xls OR filetype:xlsx

cache:domain.com       # View Google's cached version of a page (if available).

related:domain.com     # Find sites Google considers related to domain.com.

link:domain.com        # Find pages linking to domain.com (limited results nowadays).
```

## Combining Operators for Powerful Queries

_Operators can be chained together to create highly specific searches._

```
# Find PDF reports mentioning "strategy" on Norwegian government sites
site:*.gov.no filetype:pdf "strategy" OR "strategi"

# Find potential login pages on a specific domain
site:example.com intitle:login OR inurl:signin OR inurl:auth

# Find Excel spreadsheets containing "employee list" but exclude templates
filetype:xlsx "employee list" -template

# Find directory listings containing backups
intitle:"index of" "backup" OR "dump"
```

## OSINT Dork Examples

```
# Finding Files & Documents
site:*.no filetype:pdf "årsrapport" OR "annual report"         # Find annual reports on .no sites
site:company.com filetype:xlsx "budget" OR "forecast"         # Find budget spreadsheets on company site
filetype:log "password" OR "username" site:example.com        # Find logs mentioning credentials (Use Ethically!)
filetype:sql OR filetype:bak "database dump" OR "backup"       # Search for database backup files
site:edu.no filetype:ppt "research project"                   # Find presentations on Norwegian edu sites

# Finding Login / Admin Portals
intitle:"Login" OR intitle:"Sign In" inurl:admin OR inurl:login # Common login patterns
site:internal.company.com intitle:"Login"                     # Target potential internal portals (if indexed)
inurl:/remote/login                                           # Specific path for remote access portals

# Finding Directory Listings (Potential Leaks)
intitle:"index of /"                                          # Generic directory listing
intitle:"index of" "/private/" OR "/confidential/"            # Search specific directory names
intitle:"index of" "backup" OR "archive"                      # Find backup directories

# Searching Specific Platforms / Social Media
site:linkedin.com/in "firstname lastname" "company name"      # Find LinkedIn profiles
site:github.com "company name" "api_key" OR "secret"          # Find potential keys on GitHub (Use Ethically!)
site:pastebin.com "company.com" OR "internal_ip"              # Find company mentions on Pastebin
site:trello.com "company name" "project roadmap" OR "password" # Find public Trello boards (Use Ethically!)
site:facebook.com/ "Person Name" "City Name" public info      # Search public Facebook info

# Finding People / Company Information
"Person Name" filetype:pdf site:company.com                   # Find PDFs mentioning a person on a company site
"Company Name" intitle:"staff directory" OR intext:"our team"  # Find employee information pages
related:company.com                                           # Find related organizations
site:company.com intitle:"internal use only" -jobs            # Find documents marked internal

# Finding Technical Information / Exposed Services
intitle:"Grafana" inurl::3000 OR inurl::8080                   # Find Grafana dashboards
intitle:"kibana" inurl::5601                                  # Find Kibana instances
inurl:/phpinfo.php intitle:"phpinfo()"                        # Find exposed phpinfo pages
intitle:"Welcome to Nginx!"                                   # Find default Nginx pages
"Apache Tomcat" intitle:"Welcome"                             # Find Apache Tomcat servers
```
