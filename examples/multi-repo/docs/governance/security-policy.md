---
id: docs-governance-security-policy
title: Security & Data-Handling Policy
type: governance
purpose: policy
status: draft
owner: security-owner
source_of_truth: false
scope: global
ai_usage: allowed
---

# Security & Data-Handling Policy

Source of truth chi tiết cho **secrets, PII, log, production data, sanitize, secret-scanning và retention**.
Topology chỉ nêu bright-line (Mục 15); chi tiết ở file này.

## 1. Bright-line (không đổi)
- Không commit secret/credential vào `docs/`, repo-level docs hoặc `.ai/`.
- Customer PII, raw production log nhạy cảm, dữ liệu thật từ production/third-party chỉ vào tài liệu/prompt
  **sau khi sanitize và có approval**.
- `.ai/outputs/` (kể cả scratch bị gitignore) vẫn phải secret-scan và có retention rule.

## 2. Phân loại dữ liệu (TODO)
Public / Internal / Confidential / Restricted (PII, secret, production data) — định nghĩa + ví dụ.

## 3. Sanitize & approval (TODO)
Quy trình sanitize; role được approve đưa dữ liệu nhạy cảm vào tool AI.

## 4. Approved tool & data boundary
Tool nào được phép, loại dữ liệu nào được đưa vào (liên kết `../platform/approved-tools.md`).

## 5. Secret-scanning & retention (TODO)
Secret-scan trong CI cho `docs/` và `.ai/`; retention/expiry cho `.ai/outputs/` và audit evidence.

## 6. Incident
TODO: xử lý khi lộ dữ liệu; ai là Incident Commander.

## Liên quan
`ai-governance.md`, `risk-level-policy.md`, `../platform/approved-tools.md`.
