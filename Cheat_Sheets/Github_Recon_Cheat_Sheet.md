# GitHub Reconnaissance Cheat Sheet

## 1. Objective

GitHub reconnaissance (recon) is the systematic discovery of sensitive information, exposed infrastructure, credentials, technologies, and attack surface from public repositories, profiles, and GitHub metadata.

---

## 2. High‑Level Recon Workflow

1. Identify target organization/user
2. Enumerate repositories
3. Analyze commits & history
4. Extract secrets & credentials
5. Map infrastructure
6. Identify developers & access patterns
7. Correlate external assets

---

## 3. Target Enumeration

### Organization Discovery

* Search by company/domain name
* Look for verified organizations
* Check forks and mirrors

**Useful Queries**

```
org:TARGET
user:TARGET
"TARGET.com"
```

### Employee / Developer Discovery

* Contributors tab
* Commit authors
* Pull request participants
* Linked emails in commits

---

## 4. Advanced GitHub Search (Dorks)

### File Type Discovery

```
extension:env
extension:yaml
extension:yml
extension:json
extension:config
extension:ini
```

### Sensitive Keywords

```
"API_KEY"
"SECRET_KEY"
"password="
"token="
"aws_access_key_id"
"private_key"
```

### Infrastructure Clues

```
"internal"
"staging"
"prod"
"vpn"
"kubernetes"
"terraform"
```

### Example Combined Queries

```
org:TARGET "password"
org:TARGET extension:env
org:TARGET "BEGIN RSA PRIVATE KEY"
```

---

## 5. Repository Intelligence

### What to Inspect

* README files
* Wiki pages
* Issues & discussions
* Pull requests
* Branch names
* Tags & releases

### High‑Value Files

* `.env`
* `docker-compose.yml`
* `config.js`
* `settings.py`
* `application.properties`
* `.npmrc`
* `.gitlab-ci.yml`
* `.github/workflows/`

---

## 6. Commit & History Analysis

Secrets often exist in old commits even if removed.

### Manual Checks

* Commit diffs
* Reverted commits
* Force pushes

### Commands

```
git clone https://github.com/org/repo.git
git log --all
git show <commit>
git grep -i password
```

### Historical Secret Recovery

```
git log -p | grep -i "api"
```

---

## 7. Secret Hunting Tools

### Automated Tools

* trufflehog
* gitleaks
* gitrob
* repo-supervisor
* shhgit

### Example Usage

```
trufflehog git https://github.com/org/repo
```

---

## 8. GitHub API Recon

### Useful Endpoints

```
https://api.github.com/orgs/TARGET/repos
https://api.github.com/users/TARGET/repos
https://api.github.com/repos/ORG/REPO/commits
```

### Use Cases

* Repo enumeration
* Contributor extraction
* Automation pipelines

---

## 9. Metadata & Leakage Analysis

Check for:

* Email addresses
* Internal domains
* Subdomains
* Cloud storage buckets
* IP addresses

### Regex Examples

```
[A-Za-z0-9._%+-]+@TARGET.com
https?://[a-zA-Z0-9.-]*TARGET.com
```

---

## 10. CI/CD & Automation Exposure

Inspect:

* GitHub Actions workflows
* Deployment scripts
* Environment variables
* Build logs

Look for:

* Tokens
* Container registries
* Cloud credentials

---

## 11. Dependency & Supply Chain Recon

Check:

* package.json
* requirements.txt
* go.mod
* pom.xml

Identify:

* Outdated dependencies
* Internal packages
* Private registries

---

## 12. Infrastructure Mapping

Look for references to:

* AWS
* Azure
* GCP
* Kubernetes clusters
* Terraform state files

Common indicators:

```
*.amazonaws.com
*.cloudapp.azure.com
*.gcp
```

---

## 13. Developer OPSEC Weaknesses

Common leaks:

* Personal tokens
* Hardcoded credentials
* Local paths
* SSH keys
* Debug configs

Also check:

* Commit timestamps
* Time zones
* Work schedules

---

## 14. Automation & Scaling Recon

Combine with:

* Subdomain enumeration tools
* OSINT frameworks
* Bug bounty automation

Pipeline idea:

1. Enumerate org repos
2. Clone automatically
3. Run secret scanners
4. Extract domains
5. Feed into recon tools

---

## 15. Red Flags / High‑Value Findings

* Private keys
* Cloud credentials
* Database connection strings
* Internal dashboards
* Admin endpoints
* Hardcoded JWT secrets

---

## 16. Reporting & Ethics

Always:

* Follow responsible disclosure
* Respect program scope
* Avoid exploiting live data
* Document proof safely

---

## 17. Quick Command Reference

```
# clone all org repos
gh repo list ORG --limit 500 | awk '{print $1}' | xargs -L1 gh repo clone

# search locally
grep -R "password" .

# find private keys
grep -R "BEGIN RSA" .
```

---

## 18. Pro Tips

* Deleted ≠ gone (check history)
* Forks often leak more than originals
* Small repos are frequently misconfigured
* CI logs are underrated intel sources
* Developers reuse credentials

---

## 19. Legal Reminder

Use only for:

* Authorized penetration testing
* Bug bounty programs
* Defensive security research

Unauthorized access may violate laws.

---

## 20. Critical Asset Discovery Queries (GitHub Search Library)

> Use only within authorized engagements or defensive security research.

### 🔑 Credential & Secret Exposure

```
"api_key="
"API_KEY"
"SECRET_KEY"
"access_token"
"auth_token"
"client_secret"
"password="
"passwd="
"db_password"
"connectionString"
"jdbc:mysql://"
"mongodb+srv://"
```

### ☁️ Cloud Credentials & Infrastructure

```
"aws_access_key_id"
"aws_secret_access_key"
"AKIA" org:TARGET
"azure_storage_account"
"DefaultEndpointsProtocol=https"
"GOOGLE_APPLICATION_CREDENTIALS"
"gcloud auth"
"service_account.json"
```

### 🔐 Private Keys & Certificates

```
"BEGIN RSA PRIVATE KEY"
"BEGIN OPENSSH PRIVATE KEY"
"BEGIN PRIVATE KEY"
"BEGIN EC PRIVATE KEY"
".pem"
".p12"
".key"
```

### 🧭 Internal Infrastructure & Environments

```
"internal." 
"corp." 
"staging." 
"dev." 
"vpn"
"intranet"
"admin portal"
"dashboard"
"grafana"
"kibana"
```

### 🐳 DevOps / CI‑CD Exposure

```
path:.github/workflows "token"
"docker login"
"CI_JOB_TOKEN"
"deploy_key"
"kubectl apply"
"helm repo add"
"kubeconfig"
```

### 🗄️ Database & Storage Access

```
"redis://"
"postgres://"
"mysql://"
"elasticsearch"
"firebaseio.com"
"s3.amazonaws.com"
"blob.core.windows.net"
```

### 🌐 Subdomain & Asset Enumeration

```
"https://*.TARGET.com"
"api.TARGET.com"
"dev.TARGET.com"
"admin.TARGET.com"
"internal.TARGET.com"
```

### 📱 Mobile & Application Secrets

```
extension:plist "API"
extension:xml "apikey"
extension:json "client_id"
"google_maps_key"
"firebase_api_key"
```

### 🧪 Debug & Misconfiguration Leakage

```
"DEBUG=True"
"NODE_ENV=development"
"stacktrace"
"Exception at"
"console.log(password"
```

### 🧑‍💻 High‑Signal Combined Queries

```
org:TARGET extension:env
org:TARGET "BEGIN RSA"
org:TARGET "password" NOT test
org:TARGET "aws" "secret"
org:TARGET "internal" "api"
```

---

### ⚡ Analyst Tips

* Combine **org:**, **user:**, and **filename:** filters for precision.
* Search forks — sensitive data often survives there.
* Sort results by **Recently Indexed** to catch fresh leaks.
* Try lowercase + uppercase variations.
* Remove quotes to widen discovery scope after initial hits.
