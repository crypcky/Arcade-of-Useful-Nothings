# Bug Bounty Recon → Action Checklist

This checklist helps convert reconnaissance intelligence into
structured, actionable testing steps during a bug bounty engagement.

------------------------------------------------------------------------

## 1. Scope Validation

-   [ ] Confirm all discovered assets are **in-scope**
-   [ ] Identify wildcard domains or subsidiary programs
-   [ ] Verify cloud assets (AWS/GCP/Azure) ownership
-   [ ] Check for staging, dev, or legacy environments
-   [ ] Record program rules & safe-harbor constraints

------------------------------------------------------------------------

## 2. Asset Inventory & Classification

-   [ ] Categorize assets:
    -   Web applications
    -   APIs (REST / GraphQL)
    -   Mobile backends
    -   Admin panels
    -   Third‑party integrations
-   [ ] Tag technologies (frameworks, languages, servers)
-   [ ] Identify authentication surfaces
-   [ ] Map public vs internal exposure

------------------------------------------------------------------------

## 3. Attack Surface Expansion

-   [ ] Enumerate subdomains
-   [ ] Resolve historical DNS records
-   [ ] Check archived URLs (Wayback / Common Crawl)
-   [ ] Discover hidden parameters
-   [ ] Enumerate directories & endpoints
-   [ ] Identify forgotten endpoints or deprecated APIs

------------------------------------------------------------------------

## 4. Technology Fingerprinting

-   [ ] Detect frameworks and CMS versions
-   [ ] Identify JS libraries & versions
-   [ ] Look for outdated dependencies
-   [ ] Enumerate exposed headers & metadata
-   [ ] Analyze API schemas or OpenAPI docs

------------------------------------------------------------------------

## 5. Authentication & Authorization Review

-   [ ] Test login flows
-   [ ] Inspect password reset mechanisms
-   [ ] Check MFA implementation
-   [ ] Attempt privilege escalation
-   [ ] Test IDOR across discovered endpoints
-   [ ] Validate role-based access controls

------------------------------------------------------------------------

## 6. Input & Parameter Testing

-   [ ] Test query/body parameters
-   [ ] Fuzz hidden parameters
-   [ ] Attempt injection vectors:
    -   SQLi
    -   SSTI
    -   Command Injection
    -   LDAP/NoSQL Injection
-   [ ] Validate file upload functionality
-   [ ] Test deserialization points

------------------------------------------------------------------------

## 7. Client-Side Recon Usage

-   [ ] Review JavaScript files for:
    -   Hardcoded secrets
    -   API keys
    -   Hidden endpoints
-   [ ] Inspect source maps
-   [ ] Analyze WebSocket traffic
-   [ ] Review mobile app API calls

------------------------------------------------------------------------

## 8. Infrastructure & Misconfiguration Checks

-   [ ] Test CORS policies
-   [ ] Check security headers
-   [ ] Identify open storage buckets
-   [ ] Scan exposed services/ports
-   [ ] Inspect CDN and cache behavior
-   [ ] Validate rate limiting

------------------------------------------------------------------------

## 9. Data Exposure & Sensitive Information

-   [ ] Search for leaked credentials
-   [ ] Check error messages & stack traces
-   [ ] Inspect backup files
-   [ ] Look for exposed logs
-   [ ] Validate GraphQL introspection exposure

------------------------------------------------------------------------

## 10. Automation Opportunities

-   [ ] Build wordlists from recon data
-   [ ] Automate endpoint testing
-   [ ] Create custom fuzzing payloads
-   [ ] Schedule continuous monitoring
-   [ ] Track new assets automatically

------------------------------------------------------------------------

## 11. Prioritization & Reporting Prep

-   [ ] Rank findings by impact & exploitability
-   [ ] Reproduce issues consistently
-   [ ] Capture proof-of-concept evidence
-   [ ] Document affected endpoints
-   [ ] Draft remediation suggestions
-   [ ] Validate against program severity guidelines

------------------------------------------------------------------------

## 12. Operational Hygiene

-   [ ] Avoid noisy scans unless permitted
-   [ ] Respect rate limits
-   [ ] Log all testing activity
-   [ ] Maintain reproducibility notes
-   [ ] Securely store gathered intelligence

------------------------------------------------------------------------

### Notes

Use this checklist iteratively --- recon is not a one-time phase. New
findings should continuously feed back into asset discovery and testing
strategy.
