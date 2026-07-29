# AI Agent Instruction: Colz Notes Workspace Guide

Welcome, Agent! This repository is a structured collection of VLSI and Solid-State course lecture notes. To work efficiently, save context, and answer user queries accurately without brute-force searching, read and follow these guidelines.

---

## 📂 Naming Schemes of the Slides

In each course directory, the PDF slides are organized in the `lecture/` (or `Lecture/`) folder and named chronologically and topically according to one of the following schemes:
- **ASD and ADDV**: `Week_XX_Lecture_YY_Topic_Inside_Name.pdf`
- **PSD and VDF**: `Week_XX_Topic.pdf` (or `WeekXX_LY_Topic_YYYY-MM-DD.pdf`)

---

## 🔍 Using Lookup Tables (Fast Routing)

Instead of running heavy PDF text extractions across all files when a user asks a question, read the corresponding markdown **Lookup Table** first to locate the exact lecture file and slide details:

| Course / Directory | Lookup Table |
|---|---|
| Advanced Solid-State Devices | [ASD_Lookup.md](file:///Users/vs/function/Colz_notes/ASD_Lookup.md) |
| Advanced Digital Design and Verification | [ADDV_Lookup.md](file:///Users/vs/function/Colz_notes/ADDV_Lookup.md) |
| VLSI Design Flow | [VDF_Lookup.md](file:///Users/vs/function/Colz_notes/VDF_Lookup.md) |
| Physics of Semiconductor Devices | [PSD_Lookup.md](file:///Users/vs/function/Colz_notes/PSD_Lookup.md) |

### How to Use the Lookup Tables:
1. **Search**: Read the matching `*_Lookup.md` file using your file reading tools (`view_file` or `grep_search`).
2. **Locate**: Find the lecture code (e.g., `W4 L1` or `Week_04`) or matching slide titles for the user's keywords.
3. **Inspect**: Open the specific PDF file in that course's `lecture/` (or `Lecture/`) folder.
4. **Extract**: Use `view_file` on the target PDF (which converts the slides to text via OCR/extraction) to read the exact text/equations from the relevant pages.
