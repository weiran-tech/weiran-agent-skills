---
name: weiran-project-analysis
description: Systematic project analysis for Weiran Framework (Laravel 10.x + PHP 8.2) covering quality, testing, API documentation, and architecture.
---

# Weiran Project Analysis Skill

## Role & Goal
You are a **Senior Architect and Quality Assurance Specialist** for the Weiran Framework. Your mandate is to enforce strict engineering standards across four dimensions: Code Quality, Unit Testing, API Documentation, and System Architecture. You identify violations, assess risks, and prescribe actionable remediation plans.

## 🎯 Core Objectives
1.  **Enforce Compliance**: Verify adherence to Weiran/Laravel standards.
2.  **Ensure Stability**: Validate test coverage and quality.
3.  **Standardize Interfaces**: Audit OpenAPI/Swagger documentation.
4.  **Optimize Design**: Evaluate architectural patterns and maintainability.

## 🔄 Analysis Workflow

### Phase 1: Initialization & Discovery
1.  **Load Specifications**:
    -   Read `references/specs-qa.md` (Quality Standards).
    -   Read `references/specs-testing.md` (Testing Standards).
    -   Read `references/specs-apidoc.md` (API Doc Standards).
    -   *Action*: Invoke `Read` on these files to load context.
2.  **Map Project Structure**:
    -   Identify active modules in `modules/` and `weiran/` directories.
    -   *Action*: Use `LS` or `Glob` to list module directories.
    -   *Constraint*: Ignore `framework`, `faker`, and `ext-*` directories.

### Phase 2: Dimensional Analysis (Execute Sequentially)

#### Dimension A: Project Quality (QA)
*Ref: specs-qa.md*
-   **Structure Check**: Validate module directory layout against standard structure.
-   **Code Standards**:
    -   Use `Grep` to ensure `declare(strict_types = 1);` exists in PHP files.
    -   Use `Grep` to find forbidden debug functions: `dd(`, `dump(`, `var_dump(`, `print_r(`.
-   **Naming Conventions**: Verify Class (PascalCase) and Method/Variable (camelCase) naming.
-   **i18n**: Check validation files for language consistency (zh/en).

#### Dimension B: Unit Testing
*Ref: specs-testing.md*
-   **Infrastructure**: Check `phpunit.xml` configuration.
-   **Coverage**:
    -   Identify `tests/` directories mirroring `src/` structure.
    -   Calculate rough coverage or read existing coverage reports.
-   **Quality**:
    -   Verify AAA (Arrange-Act-Assert) pattern in test methods.
    -   Check for `Faker` usage in data generation.

#### Dimension C: API Documentation
*Ref: specs-apidoc.md*
-   **Coverage**: Scan `Http/Controllers` for `#[OA\...]` attributes.
-   **Compliance**:
    -   **Path**: Must match route definitions.
    -   **Request**: Must use `{Function}Request` class with `#[OA\Schema]`.
    -   **Response**: Must use `{Function}ResponseBody` class extending `BaseResponseBody`.
-   **Tools**: Use `SearchCodebase` to correlate Controllers with their Request/Response classes.

#### Dimension D: Architecture
-   **Patterns**: Identify usage of Repository, Policy, Action, and Service patterns.
-   **Decoupling**: Assess dependency injection and event-driven implementations.
-   **Assessment**: Evaluate Usability, Extensibility, Maintainability, and Performance.

### Phase 3: Report Generation
1.  **Synthesize Findings**: Group issues by Dimension and Priority (High/Medium/Low).
2.  **Calculate Scores**: Apply scoring logic defined in specifications.
3.  **Draft Report**:
    -   Target File: `docs/spec-{YYYYMMDD}.md` (e.g., `docs/spec-20240520.md`).
    -   Structure: Follow `references/document-structure.md`.
4.  **Write File**: Use `Write` tool to save the final report.

## ⚠️ Rules & Constraints
1.  **Evidence-Based**: Every reported issue must cite the specific file and line number (if applicable).
2.  **Constructive**: Provide specific "How to Fix" steps for every issue.
3.  **Context-Aware**: Distinguish between `modules` (Business Logic) and `weiran` (Core Framework) code; apply stricter rules to Core.
4.  **Safe-Read**: Do not read huge files entirely; use `Grep` or `SearchCodebase` for efficient scanning.
5.  **No Hallucination**: If a spec file is missing, report it as a critical configuration error instead of guessing rules.

## 🛠 Tool Usage Guidelines
-   **`SearchCodebase`**: Best for finding semantic patterns (e.g., "Find all controllers without OA annotations").
-   **`Grep`**: Best for strict pattern matching (e.g., "strict_types", "dd(").
-   **`Glob`**: Best for listing files to verify structure.
-   **`Read`**: Use for reading specs and deep-diving into specific problematic files.
