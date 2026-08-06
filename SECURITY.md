- [Security Policy](#security-policy)
  - [Supported Versions](#supported-versions)
  - [Reporting a Vulnerability](#reporting-a-vulnerability)
  - [What to Include](#what-to-include)
  - [Our Commitment](#our-commitment)
  - [Scope](#scope)
  - [Safe Harbor](#safe-harbor)

# Security Policy

This policy applies to **all repositories in the FalkorDB organization**, including
the FalkorDB graph database and every client library, tool and integration we
publish.

## Supported Versions

We release patches for security vulnerabilities. Which versions are eligible for
receiving such patches depends on the CVSS v3.0 Rating:

| CVSS v3.0 | Supported Versions                        |
| --------- | ----------------------------------------- |
| X.Y.Z     | Releases within the previous three months |
| X.Y.Z     | Most recent release                       |

## Reporting a Vulnerability

Please report (suspected) security vulnerabilities to
**[security@falkordb.com](mailto:security@falkordb.com)**. You will receive a response from
us within 48 hours. If the issue is confirmed, we will release a patch as soon
as possible depending on complexity but historically within a few days.

You may also report privately through GitHub by opening a draft security advisory
on the affected repository, under **Security → Advisories → Report a vulnerability**.

**Please do not report security vulnerabilities through public GitHub issues,
discussions, or pull requests.**

## What to Include

To help us triage quickly, please include as much of the following as you can:

- The type of issue (buffer overflow, injection, privilege escalation, and so on)
- The affected repository, version or commit SHA
- Full paths of the source files related to the issue
- Step-by-step instructions to reproduce
- Proof-of-concept or exploit code, if available
- The impact of the issue, including how an attacker might exploit it

## Our Commitment

When you report a vulnerability to us, we will:

1. Acknowledge receipt within **48 hours**.
2. Confirm the issue and determine its severity using CVSS v3.0.
3. Keep you informed of remediation progress.
4. Remediate according to our published timelines — **High: 3 days,
   Medium: 7 days, Low: 30 days** — from confirmation.
5. Publish a GitHub Security Advisory and credit you for the discovery, unless
   you prefer to remain anonymous.

## Scope

This policy covers the repositories published under the
[FalkorDB organization](https://github.com/FalkorDB).

For vulnerabilities in **FalkorDB Cloud** (`app.falkordb.cloud`), please use the
same contact address. Findings in third-party infrastructure providers should be
reported to the relevant provider, though we appreciate being informed.

The following are generally **out of scope**:

- Reports from automated scanners without a demonstrated, exploitable impact
- Denial of service achieved purely through resource exhaustion by an
  authenticated and authorized user acting within their granted privileges
- Missing security headers or TLS configuration issues with no demonstrated impact
- Social engineering of FalkorDB staff or customers
- Vulnerabilities requiring physical access to a user's device

## Safe Harbor

We consider security research conducted in good faith under this policy to be
authorized. We will not pursue or support legal action against researchers who:

- Make a good faith effort to avoid privacy violations, data destruction, and
  interruption or degradation of our services
- Only interact with accounts they own or have explicit permission to access
- Report promptly and do not exploit a finding beyond what is necessary to
  demonstrate it
- Give us reasonable time to remediate before public disclosure
