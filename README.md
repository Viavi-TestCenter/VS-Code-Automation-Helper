# VS‑Code‑Automation‑Helper
> Viavi TestCenter & ONE LabPro VS Code Automation Helper Collection

## Overview
This repository contains four independent VS Code helper extensions for **Viavi TestCenter** and **ONE LabPro** automation scripting. All extensions are compatible with VS‑Code‑architecture editors, including VS Code, Trae, Cursor, Qoder, Code Buddy, Devin.

These extensions address the complexity of weakly‑typed or deeply‑nested test‑automation APIs. They deliver context‑aware auto‑completion, structured hover documentation, signature hints, and collections of ready‑to‑use code snippets, helping test engineers improve script quality and accelerate test automation development.

### Included Projects (4 Repository Sub‑Folders)
| Folder | Product | Target API |
|---|---|---|
| `TestCenter Native API Automation Helper` | Viavi TestCenter | Native Python (StcPython) API |
| `ONE LabPro pyapi Automation Helper` | Viavi ONE LabPro | ONE LabPro Python Object‑Tree API |
| `TestCenter RESTful API Automation Helper` | Viavi TestCenter | TestCenter REST HTTP API |
| `TestCenter Snappi API Automation Helper` | Viavi TestCenter | Open Traffic Generator Snappi API |

> **ONE LabPro**: VIAVI high‑speed Ethernet test platform for high‑rate interface testing, PHY/FEC validation, L2‑L3 traffic simulation, transceiver management and AI‑HPC network test scenarios.

## Common Features Across All Helpers
All extensions share consistent design patterns and adopt lazy‑loading activation: they only load schema data when opening Python (`*.py`) files to minimize idle memory consumption.

- **Rich built‑in code snippets & templates**: Reusable complete test scripts and function fragments. Each snippet uses unique naming prefixes to avoid conflicts when multiple extensions are installed side‑by‑side.
- **Multiple snippet insertion workflows**:
  1. Inline trigger: type `#` (and `##` for function fragments in ONE LabPro helper) at the start of a line in Python files to bring up completion suggestion list.
  2. Full snippet prefix + `Tab` quick expansion.
  3. Hierarchical template picker via keyboard shortcut (available for TestCenter series extensions).
- **Context‑aware inference engine**: Analyzes source code to resolve object handle and API node types, supports variable alias tracking and multi‑line call parsing, filters completion suggestions according to actual object context.
- **Intelligent auto‑completion**: Provides hints for object classes, API methods, commands, parameters and enum values. Some extensions support automatic import statement injection.
- **Structured hover documentation**: Markdown‑style documentation cards showing API path, data type, default value, enum options and feature support status.
- **Signature help**: Pop‑up parameter hints when typing opening parenthesis `(` for function/method calls.
- **Offline VSIX installation**: No marketplace required. Extensions can be deployed locally via compiled `.vsix` packages on any compatible editor.

## Installation Guide (Offline VSIX)
All extensions follow the same installation workflow:
1. Open your editor and navigate to Extensions panel (`Ctrl+Shift+X`).
2. Click `···` icon at top‑right corner → **Install from VSIX…**.
3. Select target `.vsix` file, finish installation and restart editor.

> **Update / Reinstall**: Uninstall existing extension, restart editor, then install new VSIX package. Some editors support direct over‑installation without manual uninstall.
>
> Some editors support command‑line installation:
> ```bash
> code --install-extension your‑extension‑file.vsix
> ```

## Snippet Usage Workflow for Python (`*.py`)

### Method 1: Inline trigger (Recommended)
1. At the beginning of a line, type `#` (for full test scripts); ONE LabPro helper additionally supports `##` for lightweight function‑call fragments.
2. The completion popup lists matching templates. Input keywords to filter candidates.
3. Press `Enter` or `Tab` to insert the full snippet; trigger symbol will be automatically stripped.
4. Navigate placeholders:
    - `Tab`: jump to next placeholder
    - `Shift+Tab`: jump to previous placeholder
    - `Esc`: exit placeholder navigation mode

### Method 2: Full prefix + Tab
Type the complete snippet prefix name, then press `Tab` to expand into runnable code.

### Method 3: Hierarchical template picker (TestCenter‑series extensions only)
1. Place cursor at desired insertion position inside Python file.
2. Use shortcut `Ctrl+Shift+I`, or open command palette and run `TC: Insert Code Template`.
3. Select category and target snippet from the pop‑up list.

> After snippet expansion, remember to fill in environment‑related placeholders such as chassis / controller IP, slot‑port locations, MAC and IP addresses before executing scripts.

## Environment Prerequisites
> ⚠️ All helpers are **pure front‑end syntax‑assistance tools**. They do NOT contain test runtime engine. Generated Python scripts require separate runtime environment to execute properly.

Each extension corresponds to its own runtime dependencies:
- **TestCenter Native API Helper**: Requires Viavi TestCenter environment and accessible test chassis.
- **TestCenter RESTful API Helper**: Requires `stcrestclient` Python library and running TestCenter Lab Server.
- **TestCenter Snappi API Helper**: Requires `snappi` Python package and accessible TestCenter OTG service endpoint.
- **ONE LabPro pyapi Helper**: Requires ONE LabPro Python SDK and reachable ONE LabPro controller.

> Extensions themselves work completely offline. All API schema and snippet resources are packaged inside VSIX, no network connection needed for auto‑completion and hover documentation.

## Repository Structure
```
VS‑Code‑Automation‑Helper/
├── TestCenter Native API Automation Helper/         # Source for TestCenter Native Python helper
├── ONE LabPro pyapi Automation Helper/    # Source for ONE LabPro pyapi helper
├── TestCenter RESTful API Automation Helper/         # Source for TestCenter REST API helper
└── TestCenter Snappi API Automation Helper/          # Source for Snappi OTG API helper
```
Each sub‑directory is a fully independent VS Code extension project, including source code, API schema files, snippet definitions, per‑component readme documents and build scripts for generating `.vsix` packages.

## Build VSIX Locally
> Require Node.js and `vsce` toolchain.
```bash
# Enter target extension folder
cd "TestCenter Native API Automation Helper"
npm install
vsce package
```
The compiled `.vsix` file will be generated inside each sub‑folder for offline installation.

## Feedback & Technical Support
For bug reports, feature suggestions, new snippet requirements or schema update requests for new product firmware releases:
- Support Email: `HSESupportBJ@viavisolutions.com`

Feedback scope includes but not limited to:
- Issues of auto‑completion, hover documentation and signature hints
- Requests for new test‑scenario snippets
- Editor compatibility problems
- API schema alignment for new TestCenter / ONE LabPro versions

## Roadmap
- Keep embedded API schemas synchronized with new Viavi TestCenter and ONE LabPro firmware releases.
- Continuously enrich built‑in snippet library for more test scenarios.
- Optimize inference engine capability for more complex code patterns.
- Improve cross‑editor compatibility.
