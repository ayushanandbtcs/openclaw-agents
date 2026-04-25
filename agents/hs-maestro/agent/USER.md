# USER.md - About Your Human

- **Name:** Ayush Anand
- **What to call them:** Ayush
- **Timezone:** Asia/Calcutta (IST, UTC+5:30)

## Context

Ayush works on Hyperswitch — an open-source payment orchestration platform built in Rust, maintained by Juspay.

### Project Profile

- **Project:** Hyperswitch — Open-source payment orchestration platform
- **Repo:** `~/hyperswitch` (monorepo, 40+ crates)
- **Language:** Rust (Edition 2021, MSRV 1.85.0)
- **Framework:** Actix-web 4.x, Tokio async runtime
- **Database:** PostgreSQL (Diesel ORM), Redis
- **Build tool:** `just` (justfile) + `cargo`

### Preferences

- **Quality Bar:** Production-grade payment infrastructure — not prototypes
- **Architecture Style:** Domain-driven design, trait-based polymorphism
- **Code Style:** Idiomatic Rust, zero-cost abstractions, no `unwrap` in production paths
- **Compliance Awareness:** PCI-DSS Level 1
- **Communication:** Direct, no filler — just tell him what's happening and what's next

### What Ayush Wants from Galileo

- **One dispatch:** Send everything to OpenCode. No separate agents for planning, review, compile.
- **Two checkpoints:** Ask approval after plan, ask to verify after build. Nothing else.
- **No noise:** Only surface the final result or escalate if stuck after 3 attempts.
- **Test scripts:** Every task must produce a `test_changes.sh` with curl commands for manual verification.
- **No subagents:** Never spawn your own subagents. Only OpenCode via ACP.

---

The more you know, the better you can help. Build this over time.
