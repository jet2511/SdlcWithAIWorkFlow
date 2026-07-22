# SDLC With AI Workflow

Tập hợp bộ Quy trình Vận hành Chuẩn (SOP - Standard Operating Procedures) quy định mô hình phát triển phần mềm **Spec-Driven & Test-Driven SDLC** phối hợp giữa **Con người (Engineering Team)** và **AI Agents / Subagents**.

---

## 1. Danh Mục Tài Liệu SOP

| Tài liệu SOP | Vai trò | Trách nhiệm chính |
| :--- | :--- | :--- |
| 👑 [sop_tech_lead_orchestrator.md](file:///d:/Projects/Personal/AI/_pet/SdlcWithAIWorkFlow/sop_tech_lead_orchestrator.md) | **Tech Lead / System Architect** | Điều phối liên vai trò (Cross-role Orchestration), duyệt API Contract, quản lý Spec Drift & Deprecation Policy |
| 📄 [sop_ba_ai_workflow.md](file:///d:/Projects/Personal/AI/_pet/SdlcWithAIWorkFlow/sop_ba_ai_workflow.md) | **Business Analyst (BA)** | Chuyển đổi Yêu cầu thành BDD Given-When-Then, Mermaid Diagrams, Security Matrix & Versioning |
| ⚙️ [sop_backend_ai_workflow.md](file:///d:/Projects/Personal/AI/_pet/SdlcWithAIWorkFlow/sop_backend_ai_workflow.md) | **Backend Engineer** | Lập Plan API/DB, TDD Red-Green-Refactor, phòng chống N+1 query, Rollback Plan & Subagent Audit |
| 🎨 [sop_frontend_ai_workflow.md](file:///d:/Projects/Personal/AI/_pet/SdlcWithAIWorkFlow/sop_frontend_ai_workflow.md) | **Frontend Engineer** | Phủ 5 UI States, MSW API Mocking, Type-safe Component Scaffolding, Visual Check & Core Web Vitals |
| 🧪 [sop_qa_qc_ai_workflow.md](file:///d:/Projects/Personal/AI/_pet/SdlcWithAIWorkFlow/sop_qa_qc_ai_workflow.md) | **QA / QC Engineer** | Test Matrix, Automation Playwright/API/Security Scripts, Visual Regression & Cross-role RCA Bug Escalation |

---

## 2. Mô Hình Tổng Quan Luồng Làm Việc (End-to-End SDLC Flow)

```mermaid
flowchart TD
    TL_User[Tech Lead / PO Human] <--> TL_Agent[Tech Lead AI Orchestrator]
    
    subgraph Phase 1: Requirements & Security Specification
        BA_User[BA Human] <--> BA_Agent[BA AI Agent]
        BA_Agent -->|Export Spec PRD_v1.x.md| TL_Agent
    end

    subgraph Phase 2: Parallel Implementation & Contract Verification
        TL_Agent -->|Approved Spec & API Contract| BE_Agent[Backend AI Agent]
        TL_Agent -->|Approved Spec & MSW Mock| FE_Agent[Frontend AI Agent]
        TL_Agent -->|Test Matrix & BDD Specs| QA_Agent[QA/QC AI Agent]
    end

    subgraph Phase 3: Dual-Layer Audit & Verification
        BE_Agent <--> Sub_BE[Subagents: code-reviewer & security-auditor]
        FE_Agent <--> Sub_FE[Subagent: web-performance-auditor]
        QA_Agent <--> Sub_QA[Subagent: test-engineer]
    end

    subgraph Phase 4: Sign-off & Production Release
        BE_Agent -->|Walkthrough + Test Pass Logs| TL_User
        FE_Agent -->|Walkthrough + UI Screenshots| TL_User
        QA_Agent -->|Quality Sign-off / RCA Bug Report| TL_User
    end
```

---

## 3. Khung Thư Mục Cấu Trúc Dự Án Tiêu Chuẩn (Standard Repository Context)

Để các AI Agents tiếp nhận ngữ cảnh (Context) một cách nhất quán, mọi dự án áp dụng quy trình này nên được tổ chức theo cấu trúc sau:

```text
<project-root>/
├── .gemini/
│   ├── rules/                        # Quy tắc mã nguồn & bảo mật dự án
│   │   ├── global_rules.md           # Quy tắc chung (Tone, Defensive coding, Logging)
│   │   ├── backend_guidelines.md     # Chuẩn SOLID, JPA/Hibernate, Transaction rules
│   │   ├── frontend_guidelines.md    # Chuẩn React, Tailwind CSS, State management
│   │   └── security_rules.md         # Chuẩn OWASP Top 10, PII Masking & XSS
│   └── skills/                       # Tri thức kiến trúc tái sử dụng cho Agent
│       ├── project-architecture/     # Sơ đồ phân tầng & Controller-Service-Repo map
│       └── unit-testing/             # Patterns viết unit & integration test
├── docs/
│   ├── specs/                        # Tài liệu PRD_v1.x.md & Mermaid diagrams từ BA
│   ├── test-matrices/                # Test matrices & E2E script specs từ QA
│   └── walkthroughs/                 # Bằng chứng nghiệm thu (Walkthrough logs, UI screenshots)
├── sop_tech_lead_orchestrator.md
├── sop_ba_ai_workflow.md
├── sop_backend_ai_workflow.md
├── sop_frontend_ai_workflow.md
└── sop_qa_qc_ai_workflow.md
```
