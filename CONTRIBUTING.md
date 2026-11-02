# Contributing to VaxResilience

Thank you for your interest in contributing to VaxResilience! This guide will help you understand how to contribute effectively to this project.

## Project Purpose

VaxResilience is an enterprise-grade AI-powered pharmaceutical supply-chain resilience platform designed for hackathon demonstration. The project uses synthetic data to showcase how AI agents can help pharmaceutical companies detect disruptions, coordinate recovery operations, and make informed decisions under human supervision.

## Before You Start

### Required Reading

Before contributing any code or documentation:

1. **Read [AGENTS.md](AGENTS.md)** — Contains critical instructions for all AI coding agents and developers
2. **Read [README.md](README.md)** — Provides project overview and context
3. **Review relevant documentation** in `docs/` for the feature you're working on
4. **Check current project status** to understand what has been implemented

### Important Principles

- **Human oversight is mandatory** — Never implement autonomous execution of high-impact actions
- **Use SAP technology stack** — Follow the specified SAP ecosystem (SAPUI5, CAP, HANA Cloud, etc.)
- **Synthetic data only** — All demonstration data must be clearly labeled as synthetic
- **Security first** — Never commit secrets, credentials, or sensitive information

## Repository Organization

```
VaxResilience/
├── README.md              # Project overview
├── AGENTS.md              # AI coding agent instructions
├── CONTRIBUTING.md        # This file
├── docs/                  # Project documentation
│   ├── 00_PROJECT_OVERVIEW.md
│   ├── 01_BUSINESS_PROBLEM.md
│   ├── 02_DEMO_SCENARIO.md
│   └── [future documentation phases]
├── src/                   # Source code (when implementation begins)
├── data/                  # Synthetic demonstration data
└── prompts/               # AI agent prompts
```

## Getting Started

### 1. Set Up Your Environment

```bash
# Clone the repository
git clone https://github.com/Pavan-Gowda-S/VaxResilience.git
cd VaxResilience

# Check current branch
git branch

# Install dependencies (when application code exists)
npm install
```

### 2. Understand Current State

```bash
# Check what exists in the repository
git status

# Review recent changes
git log --oneline -10

# Check existing documentation
ls docs/
```

### 3. Choose What to Work On

- Review open issues (if any)
- Check project documentation for planned features
- Discuss your intended contribution with the team
- Ensure your work aligns with the current project phase

## Contribution Workflow

### 1. Create a Feature Branch

```bash
# Create and switch to a new branch
git checkout -b feature/your-feature-name

# Or for bug fixes
git checkout -b fix/bug-description
```

**Branch naming conventions:**
- `feature/` — New functionality
- `fix/` — Bug fixes
- `docs/` — Documentation updates
- `refactor/` — Code refactoring
- `test/` — Test additions or improvements

### 2. Make Your Changes

#### Code Changes

- Follow SAP development best practices
- Write clean, maintainable, modular code
- Add comments for non-obvious logic
- Implement proper error handling
- Consider performance and security
- Test your changes thoroughly

#### Documentation Changes

- Use clear, professional Markdown
- Keep terminology consistent with existing docs
- Update related documentation files
- Maintain accurate cross-references
- Follow documentation structure established in Phase 1

### 3. Test Your Changes

```bash
# Run tests (when test suite exists)
npm test

# Run linters (when configured)
npm run lint

# Test with synthetic demonstration data only
```

**Testing Requirements:**
- Test with synthetic data only
- Verify approval workflows function correctly
- Test error handling and edge cases
- Ensure audit trails are created properly
- Never use real pharmaceutical data

### 4. Commit Your Changes

```bash
# Check what will be committed
git status
git diff

# Stage specific files (preferred over git add .)
git add path/to/file1.js path/to/file2.js

# Create commit with clear message
git commit -m "feat: add inventory dashboard component

Implements the inventory visualization module showing current
stock levels, consumption rates, and supply exposure timeline.

Co-Authored-By: Claude <noreply@anthropic.com>"
```

**Commit message guidelines:**
- Use present tense ("add feature" not "added feature")
- Focus on "why" rather than "what"
- Keep first line under 72 characters
- Add detailed explanation if needed
- Reference related issues if applicable

**Commit prefixes:**
- `feat:` — New feature
- `fix:` — Bug fix
- `docs:` — Documentation changes
- `refactor:` — Code refactoring
- `test:` — Test additions
- `chore:` — Build process or tool changes

### 5. Push Your Branch

```bash
# Push to remote repository
git push -u origin feature/your-feature-name
```

### 6. Create a Pull Request

```bash
# Using GitHub CLI (preferred)
gh pr create --title "Add inventory dashboard component" --body "$(cat <<'EOF'
## Summary
- Implements inventory visualization showing stock levels and consumption
- Adds supply exposure timeline chart
- Integrates with SAP HANA Cloud data layer

## Changes
- Created `InventoryDashboard.view.xml` SAPUI5 view
- Implemented `InventoryController.js` with data binding
- Added inventory service endpoints in CAP backend
- Updated documentation in docs/DASHBOARD_AND_UI_SPECIFICATION.md

## Testing
- [x] Tested with synthetic BharatMed demonstration data
- [x] Verified chart rendering in light and dark modes
- [x] Confirmed data updates reflect in real-time
- [x] Validated error handling for missing data

## Documentation
- [x] Updated relevant documentation files
- [x] Added code comments for complex logic
- [x] Maintained consistent terminology

🤖 Generated with [Claude Code](https://claude.com/claude-code)
EOF
)"
```

**Pull Request Guidelines:**
- Keep PRs focused on a single feature or fix
- Provide clear description of changes
- List what was tested
- Update documentation in the same PR
- Keep PR size manageable for review
- Avoid mixing unrelated changes

## Code Quality Standards

### SAPUI5 (Frontend)

```javascript
// Use proper controller structure
sap.ui.define([
    "sap/ui/core/mvc/Controller",
    "sap/ui/model/json/JSONModel"
], function (Controller, JSONModel) {
    "use strict";

    return Controller.extend("com.vaxresilience.controller.Dashboard", {
        onInit: function () {
            // Initialize component
        },
        
        // Event handlers with clear names
        onRefreshData: function () {
            // Handle refresh
        }
    });
});
```

### SAP CAP (Backend)

```javascript
// Use proper service definitions
module.exports = (srv) => {
    srv.on('READ', 'Inventory', async (req) => {
        try {
            // Business logic with error handling
            const inventory = await SELECT.from('Inventory')
                .where({ facilityId: req.data.facilityId });
            
            return inventory;
        } catch (error) {
            req.error(500, 'Failed to retrieve inventory', error);
        }
    });
};
```

### Security Requirements

```javascript
// WRONG — Never expose credentials
const apiKey = "sk-1234567890abcdef";

// RIGHT — Use environment variables
const apiKey = process.env.SAP_AI_CORE_API_KEY;

// WRONG — No input validation
const userId = req.params.id;

// RIGHT — Validate all inputs
const userId = req.params.id;
if (!userId || typeof userId !== 'string') {
    return req.error(400, 'Invalid user ID');
}
```

## Documentation Standards

### Markdown Formatting

```markdown
# Main Title

## Section Heading

### Subsection

Use **bold** for emphasis, *italic* for terms, and `code` for technical references.

- Bullet points for lists
- Keep items parallel in structure
- Use consistent punctuation

| Column 1 | Column 2 |
|----------|----------|
| Data     | Data     |

[Link to related doc](docs/RELATED.md)
```

### Technical Writing

- Use clear, precise language
- Explain technical terms when helpful
- Avoid unnecessary jargon
- Keep sentences concise
- Use active voice
- Maintain consistent terminology

## What to Avoid

### Security

❌ **DO NOT:**
- Commit `.env` files or secrets
- Include credentials or tokens
- Expose API keys in frontend code
- Push sensitive configuration files
- Include real pharmaceutical data

### Code Quality

❌ **DO NOT:**
- Replace SAP technologies without approval
- Bypass human approval workflows
- Implement autonomous high-impact actions
- Add unnecessary dependencies
- Write code without error handling
- Skip testing

### Data Handling

❌ **DO NOT:**
- Use real pharmaceutical data
- Represent synthetic data as real
- Make unverified medical claims
- Claim actual patient outcomes
- Test with real supplier systems

## Human Approval Requirements

The following actions **ALWAYS require human approval** and must never be automatically executed:

1. Purchasing from alternative suppliers
2. Transferring inventory between warehouses
3. Changing factory production schedules
4. Prioritizing or reallocating customer orders
5. Changing shipment routes or carriers
6. Sending major disruption notifications
7. Approving payments or financial commitments
8. Adding or changing approved suppliers

**Every code path that triggers these actions must include an approval gate.**

## Audit and Compliance

Every implementation must support:

- Complete audit trail of all actions
- Recording of user identity and timestamp
- Immutable audit logs
- Searchable audit history
- Suspicious activity flagging
- Manual override capabilities

## Getting Help

### Questions?

- Check existing documentation in `docs/`
- Review [AGENTS.md](AGENTS.md) for guidelines
- Consult [README.md](README.md) for context
- Ask teammates for clarification

### Found an Issue?

- Check if it's already reported
- Create a detailed issue description
- Include steps to reproduce
- Provide relevant logs or screenshots
- Suggest potential solutions if possible

### Need Clarification?

If you encounter:
- Conflicting requirements
- Missing specifications
- Technical blockers
- Unclear approval authority

**Document the issue and ask for guidance rather than making assumptions.**

## Code Review Process

### For Reviewers

- Verify compliance with AGENTS.md guidelines
- Check for proper approval workflows
- Validate security practices
- Confirm documentation updates
- Test with synthetic data
- Review audit trail implementation

### For Contributors

- Respond to review comments promptly
- Make requested changes
- Update documentation as needed
- Re-test after changes
- Be open to feedback

## Project Phases

VaxResilience follows a structured documentation and implementation roadmap:

- **Phase 1**: Project Foundation (Current) — Documentation baseline
- **Phase 2**: Product Requirements and User Experience
- **Phase 3**: Architecture and Technology
- **Phase 4**: AI Agents and Governance
- **Phase 5**: Data and Integrations
- **Phase 6**: Demonstration and Project Handover

Contributions should align with the current phase and planned roadmap.

## License

See LICENSE file when added.

## Contact

For questions or collaboration inquiries, please create an issue in the repository or contact the project maintainers.

---

**Remember**: VaxResilience is built on the principle that AI analyzes and recommends, but humans decide. Every contribution must respect this principle and maintain the human-in-the-loop governance model.
