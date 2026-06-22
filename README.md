# CUSTOS
CUSTOS is an autonomous agent-security framework designed to shield generative workflows from compliance violations, safety breaches, and rate exhaustion. The system uses a strict pipeline architecture: Rate Limiting → Content Policy Inspection → Cryptographic Tamper-Evident Auditing.

CUSTOS — Content Safety Execution Firewall

A unified safety gateway for AI agent operations providing policy-based content filtering, rate limiting, and tamper-evident audit logging.

Components

File	Purpose	
`policy_engine.py`	6-rule content safety evaluation	
`rate_limiter.py`	Token bucket + daily quota enforcement	
`audit_logger.py`	SHA-256 hash-chained tamper-evident logging	
`execution_firewall.py`	Main orchestrator coordinating all components	
`demo.py`	10-test validation suite	

Quick Start

```bash
# Run validation suite
python custos_mvp/demo.py

# Use in your project
from custos_mvp.execution_firewall import gate

result = gate("youtube_upload", "My video title and description...")
if result.allowed:
    proceed_with_upload()
else:
    print(f"Blocked: {result.message}")
```

Policy Rules

1. No harmful content — Weapons, explosives, dangerous instructions
2. No hate speech — Harassment, discrimination, extremist content
3. No malware — Hacking instructions, exploits, vulnerabilities
4. No PII leaks — Social security numbers, credit cards, emails
5. No financial scams — Ponzi schemes, guaranteed returns
6. No misinformation — Medical falsehoods, conspiracy theories

Architecture

```
Operation Request
       |
       v
[ Rate Limiter ] ──Token bucket + daily quotas
       |
       v
[ Policy Engine ] ──6-rule content evaluation
       |
       v
[ Audit Logger ] ──SHA-256 hash-chained logging
       |
       v
   Allowed / Blocked
```

Audit Chain Format

Every operation is logged with:
- `timestamp` — ISO 8601 UTC timestamp
- `event_type` — operation_allowed / policy_violation / rate_limited
- `details` — Human-readable description
- `prev_hash` — SHA-256 of previous entry
- `entry_hash` — SHA-256 of this entry

Chain integrity can be verified via `firewall.verify_audit_integrity()`.

CUSTOS

Named after the Latin "custos" (guardian, protector). No relation to any prior project.
