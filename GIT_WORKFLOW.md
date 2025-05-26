# Git Workflow and Standards for Code Connect

**Date:** 2025-05-27 03:59:45

This document outlines the Git workflow, standards, and conventions to be followed for the "Code Connect" project.

## 1. Repository Information

*   **GitHub Repository URL:** [https://github.com/rikkooo/code-connect.git](https://github.com/rikkooo/code-connect.git)
*   **Local Git Configuration:**
    *   Username: `rikkooo`
    *   Email: `enrico.masella@outlook.com`
    *   *(This was configured locally for the project.)*

## 2. Core Workflow Rule

*   **Always when changes are made in the Code Connect base, they will be committed and uploaded to the repository.**
*   **Untested changes will be committed to a dedicated `test` branch or a feature-specific test branch before consideration for merging into `main`.**

## 3. Branching Strategy

We will adopt a simple branching strategy:

*   **`main` Branch:**
    *   This branch represents the stable, production-ready version of the project.
    *   Direct commits to `main` are discouraged for feature development or bug fixes.
    *   Merges into `main` should come from well-tested feature branches or hotfix branches, ideally via Pull Requests.

*   **Feature Branches:**
    *   For new features or significant changes, create a new branch from `main`.
    *   Naming convention: `feature/descriptive-name` (e.g., `feature/user-authentication`, `feature/memory-bank-enhancement`).
    *   Once a feature is complete and tested, it can be merged into `main` (preferably via a Pull Request).

*   **Test Branches:**
    *   For changes that require testing before being considered stable or integrated into a feature.
    *   Naming convention: `test/descriptive-name` or `test/feature-name` (e.g., `test/new-parser-logic`, `test/user-authentication-edge-cases`).
    *   These branches can be used for experimentation and validation. Once stable, changes can be merged into a feature branch or directly into `main` if appropriate (after thorough review).

*   **Bugfix Branches (Hotfixes):**
    *   For critical bugs found in the `main` branch that need immediate attention.
    *   Create from `main`.
    *   Naming convention: `fix/descriptive-name` or `hotfix/issue-number` (e.g., `fix/login-error`, `hotfix/issue-123`).
    *   Once the fix is verified, merge back into `main` and also into any active long-running feature branches if necessary.

## 4. Commit Message Conventions

To maintain a clear and understandable commit history, we will follow a simplified version of Conventional Commits:

*   **Format:** `type: subject`
    *   `type`: Describes the kind of change:
        *   `feat`: A new feature.
        *   `fix`: A bug fix.
        *   `docs`: Documentation only changes.
        *   `style`: Changes that do not affect the meaning of the code (white-space, formatting, missing semi-colons, etc).
        *   `refactor`: A code change that neither fixes a bug nor adds a feature.
        *   `perf`: A code change that improves performance.
        *   `test`: Adding missing tests or correcting existing tests.
        *   `chore`: Changes to the build process or auxiliary tools and libraries such as documentation generation.
        *   `ci`: Changes to CI configuration files and scripts.
    *   `subject`: A concise description of the change in the present tense (e.g., "add user login endpoint", "fix incorrect calculation").

*   **Example:**
    ```
    feat: add user profile page
    fix: correct off-by-one error in pagination
    docs: update README with setup instructions
    ```

## 5. Release Process

*   Releases will be tagged on the `main` branch.
*   We will use semantic versioning (e.g., `v1.0.0`, `v1.0.1`, `v1.1.0`).
*   Tags will be pushed to the remote repository.
    *   Command: `git tag -a vX.Y.Z -m "Release version X.Y.Z"`
    *   Command: `git push origin vX.Y.Z`

## 6. General Practices

*   Commit frequently with small, logical changes.
*   Write clear and descriptive commit messages.
*   Pull the latest changes from `main` into your feature branch regularly to avoid large merge conflicts (`git pull origin main` while on your feature branch, or `git merge main`).
*   Ensure code is tested before merging to `main`.