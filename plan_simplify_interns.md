# Plan to Simplify Intern Modes and Remove Evaluation System

This document outlines the plan to consolidate multiple "Intern" modes into a single standard "Intern" mode and remove the associated XP-based evaluation system.

## I. Modify Mode Definitions

1.  **Edit `custom_modes.yaml`:**
    *   **File:** `/home/ubuntu/.config/Code - Insiders/User/globalStorage/rooveterinaryinc.roo-cline/settings/custom_modes.yaml`
    *   **Action:** Remove the YAML blocks defining the following modes:
        *   `intern-g2`
        *   `intern-g2-5`
        *   `intern-v3`
    *   **Outcome:** Only the standard `intern` and `researcher` modes (and any other non-intern modes) will remain defined in this file.

## II. Update "Code" Mode's Custom Instructions/Prompt

1.  **Edit `config/.roorules-code`:**
    *   **File:** `config/.roorules-code`
    *   **Action:**
        *   Modify line 16 (workflow item for delegation): Change `(e.g., internship-g2, internship-g2.5, internship-d3)` to refer to the standard `intern` mode, for example: `(e.g., intern)`.
        *   Remove lines 19-20 entirely (under `internship_delegation`), which describe prompting for intern performance and calling `scripts/xp_manager.py`.
    *   **Outcome:** The "Code" mode prompt will only reference the single "Intern" mode for delegation and will no longer include instructions for evaluating interns or updating an XP tracker.

## III. Decommission the Intern Evaluation System

1.  **Delete Evaluation Script:**
    *   **File:** `scripts/xp_manager.py`
    *   **Action:** Delete this Python script.
2.  **Remove Calls to Evaluation Script:**
    *   **Action:** The primary call was identified in `config/.roorules-code` (line 20) and will be removed in step II.1. A project-wide search for other calls can be performed as a precaution.
    *   The file `memory-bank/internship_tracker.json` (referenced by `scripts/xp_manager.py`) was not found, so no action is needed for it.

## IV. Documentation & Memory Bank Updates

1.  **Update Memory Bank:**
    *   Add an entry to `memory-bank/decisionLog.md` detailing the decision to consolidate intern modes and remove the XP-based evaluation system.
    *   Update `memory-bank/progress.md` to reflect the tasks involved in this plan and their completion.

## Visual Plan (Mermaid Diagram)

```mermaid
graph TD
    subgraph "A. Mode Definitions (`custom_modes.yaml`)"
        direction LR
        M_Intern["intern (slug: intern)"]
        M_InternG2["Intern G2 (slug: intern-g2)"]
        M_InternG25["Intern G2.5 (slug: intern-g2-5)"]
        M_InternV3["Intern V3 (slug: intern-v3)"]
        M_Researcher["researcher (slug: researcher)"]

        M_InternG2 -->|REMOVE| Removed1["(Removed Definition)"]
        M_InternG25 -->|REMOVE| Removed2["(Removed Definition)"]
        M_InternV3 -->|REMOVE| Removed3["(Removed Definition)"]

        style M_Intern fill:#ccffcc
        style M_Researcher fill:#ccffcc
        style Removed1 fill:#ffcccc
        style Removed2 fill:#ffcccc
        style Removed3 fill:#ffcccc
    end

    subgraph "B. Code Mode Prompt (`config/.roorules-code`)"
        CP_Old["Old Prompt (references multiple interns, XP system)"]
        CP_New["New Prompt (references standard 'Intern' mode, no XP)"]
        CP_Old -->|MODIFY| CP_New
        style CP_New fill:#ccffcc
    end

    subgraph "C. Intern Evaluation System"
        direction LR
        XP_Script["`scripts/xp_manager.py`"]
        XP_Calls["Calls to xp_manager.py (if any)"]

        XP_Script -->|DELETE| XP_Script_Removed["(Script Deleted)"]
        XP_Calls -->|REMOVE| XP_Calls_Removed["(Calls Removed)"]
        style XP_Script_Removed fill:#ffcccc
        style XP_Calls_Removed fill:#ffcccc
    end

    subgraph "D. Memory Bank Updates"
        DecisionLog["`decisionLog.md`"]
        ProgressLog["`progress.md`"]
        DecisionLog --> DU1["Log: Consolidate Interns, Remove XP"]
        ProgressLog --> PU1["Log: Task Progress/Completion"]
        style DU1 fill:#ccffcc
        style PU1 fill:#ccffcc
    end

    Removed1 --> PU1
    CP_New --> PU1
    XP_Script_Removed --> PU1