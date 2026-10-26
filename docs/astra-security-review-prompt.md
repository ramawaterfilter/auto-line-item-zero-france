# Prompt to give GPT Astra with the Git repository

Copy the following prompt into the session that has repository access.

---

Review this Shopify application for security vulnerabilities and failures that could expose or incorrectly change order data. It is deployed on Cloudflare Workers at `https://auto-line-item-zero-france.phoxnixwaterfilter.workers.dev/` and currently serves only my own France store.

Read `docs/application-security-context.md` first, then independently trace the exact repository revision. Treat that document as an architecture map, not as proof that a control works or a vulnerability exists. Follow applicable repository instructions. Do not infer the deployed revision or account settings from local config alone.

Document the architecture and trust boundaries you confirm, then examine every workflow: embedded authentication, installation/OAuth, staff permissions for reads and writes, token exchange/refresh, manual discovery/selection/execution, automatic webhooks, uninstall, retry, cancellation, queue recovery, and Google Sheets audits. Follow customer/order data and credentials through browser, Worker, D1, queues, Shopify, Google and logs.

Prioritize unauthorized order reads/edits, cross-shop access, webhook authenticity and replay, secrets, audit integrity, and behavior under crashes/concurrent processing. Check business-logic failures as well as conventional injection or browser vulnerabilities. Distinguish the owner's single-store intent from the code's ability to store multiple installations. Do not assume a UI confirmation or a 404 page is authorization.

Read the implementation before reporting a finding. For each finding provide:

1. Severity and confidence, with a plain-English description of the affected data or order behavior.
2. Exact file and line references from the reviewed revision, affected route/workflow and trust boundary.
3. Required attacker access or operational preconditions; explain whether a signed payload, valid staff session or concurrent execution is required.
4. A concrete trigger or reproducible case using synthetic data. Clearly label static inference, isolated reproduction and live evidence separately.
5. Expected behavior versus observed/source-supported behavior, with the practical impact.
6. The smallest corrective change and a meaningful regression test that would fail before the change and pass afterward.

Separate confirmed findings, source-supported potential risks needing reproduction, expected behavior and production settings that remain unknown. Avoid generic checklist findings without a concrete source-backed case. Never say all vulnerabilities have been found or that passing tests proves security.

Start with repository inspection and local checks that do not touch external data. For tests involving external services, use synthetic data and isolated mocks or test services. This prompt does not authorize production mutation, webhook replay, uninstall, automation changes, load testing, deployments, secret rotation, or order edits. Ask me before live testing and state the exact target and side effects. Never print secrets, raw tokens, private keys or real customer data. Do not change application code as part of the review unless I separately ask for fixes.

Before testing any uncertain business rule, ask concise follow-up questions. You may continue independent source review while awaiting answers. Request secret names or redacted configuration evidence rather than secret values.

Deliver a prioritized report, a workflow/data-flow coverage matrix, regression-test specifications for supported findings, and an explicit list of what you could not verify. Record the commit, test commands and outcomes, and whether each piece of evidence came from source, a local test, an isolated integration or production.

---
