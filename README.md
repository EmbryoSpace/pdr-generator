# PDR Generator

> From an SRR/SDR package to a board-ready Preliminary Design Review draft — in hours, not months.

![Latest release](https://img.shields.io/github/v/release/EmbryoSpace/pdr-generator) ![Platform](https://img.shields.io/badge/platform-Windows%2010%2F11-0b3d66) ![Offline](https://img.shields.io/badge/runs-100%25%20offline-2a72ab)

**PDR Generator** turns your System Requirements Review (SRR) / System Definition Review (SDR) package into a complete, traceable Preliminary Design Review (PDR) draft. It runs entirely on your Windows machine — no cloud, no accounts, no telemetry.

🌐 **[embryospace.com](https://embryospace.com)**

---

## ⬇️ Download

**[⬇ Download the latest release for Windows 10/11](https://github.com/EmbryoSpace/pdr-generator/releases/latest/download/PDR-Generator-Setup.exe)**  (~112 MB)

All versions and release notes: **[Releases →](https://github.com/EmbryoSpace/pdr-generator/releases)**

> **First launch:** if Windows SmartScreen appears, click **More info → Run anyway**. (The installer is not yet code-signed.)

Free **14-day trial** — no account required.

---

## What it does

Drop in your review package — PowerPoint, Word, PDF, Excel, or CAD — and PDR Generator:

- **Extracts** every requirement (SYS-xxxx and friends), risk, TBD/TBR item, and interface, preserving the source location of each artifact.
- **Analyzes** what a review board will find: conflicting requirement definitions, missing verification methods, unallocated requirements, open TBX items, missing budgets.
- **Generates** a 17-section PDR draft built to **NASA NPR 7123.1D**, **IEEE 15288.2**, and **ECSS** — every sentence cited back to your source slides, each block carrying a confidence score.
- **Edits** in a Notion-style editor; your manual edits survive regeneration when new documents arrive.
- **Exports** to Microsoft Word, PDF, PowerPoint review slides, Markdown, and HTML.

It produces a **draft** — a traceable starting point. You bring the engineering judgment and the sign-off.

---

## Built for controlled programs

Everything runs and stays on your machine. No cloud backend, no telemetry, no accounts — **ITAR/EAR-friendly by architecture, not by promise.** Optional AI analysis uses your own API key and is off by default. A built-in "Erase all local data" control and an uninstall-time data-removal prompt let you purge everything when you need to.

See our [Privacy Policy, Terms & Export-Control notices](https://embryospace.com/legal.html).

---

## Quick start

1. **Install** and open PDR Generator.
2. **Create a project.**
3. **Import** your SRR/SDR files (drag-and-drop, multiple at once).
4. Click **Analyze** to run the gap & consistency checks.
5. Click **Generate PDR** for the full draft.
6. Review and edit in-app, then **Export** to your format.

📄 **[Formatting Guide](FORMATTING-GUIDE.md)** — how to structure your package so
it extracts cleanly · ❓ **[FAQ](FAQ.md)**

---

## Getting the best results

A few habits make a large difference. The full detail is in the
[Formatting Guide](FORMATTING-GUIDE.md); the short version:

- **Use .pptx or .xlsx for risk registers and budgets.** Only those two preserve
  table structure — a risk register inside a PDF is flat text and won't extract.
- **Give every requirement an ID with a separator and a modal verb:**
  `SYS-0101 The spacecraft shall …`. `SYS 0101` (space only) is not treated as an ID.
- **State allocations with a number and a unit:** *"dry mass shall not exceed
  240 kg"*. This is what the Decisions tab measures against.
- **State margin requirements as percentages:** *"shall maintain a dry mass margin
  of at least 15%"* — your own limit outranks the industry guideline.
- **Number your TBD/TBR items** (`TBD-07`), and put them inside the requirement
  they affect.
- **Import the source package, not a PDR this tool generated.**

> If an import returns zero requirements, it's nearly always the ID format or a
> re-imported output document — see the [FAQ](FAQ.md).

---

## Pricing

| Plan | Price | For |
|---|---|---|
| **Student** | Free (.edu verification) | University CubeSat & capstone teams |
| **Professional** | $1,800 / engineer / year | Individual engineers |
| **Team** | $12,000 / site / year | Unlimited seats at one program site |
| **Enterprise** | Custom | Multi-site programs / primes |

Start a trial or buy at **[embryospace.com](https://embryospace.com)**.

---

## License keys & support

After purchase you'll receive an offline license key by email — open the app, click **License** in the sidebar, and paste it in. Students can request a free key from the website.

Questions or issues: **[support@embryospace.com](mailto:support@embryospace.com)**

---

<sub>© 2026 Embryo Space Inc., a Delaware corporation. PDR Generator is provided "AS IS"; see the [legal notices](https://embryospace.com/legal.html). This repository hosts official release downloads and release notes only.</sub>
