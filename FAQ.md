# PDR Generator — FAQ

## General

**What does it actually do?**
You import your SRR/SDR package. It extracts requirements, risks, TBD/TBR items,
interfaces and budgets with the source location of each, runs the checks a review
board runs, and generates a 17-section PDR draft built to NASA NPR 7123.1D,
IEEE 15288.2 and ECSS — every block cited back to your source. You edit anything
in the app and export to Word, PDF, PowerPoint, Markdown or HTML.

**Is the output ready to submit?**
No. It is a *draft* — a traceable starting point, not a substitute for
engineering judgement. Every block carries a confidence score and citations so
you can check it. You review, correct, and own the result.

**Does it replace my systems engineer?**
No. It removes the assembly work — pulling requirements out of hundreds of
slides, rebuilding the traceability matrix, formatting for the board — so your
engineers spend their time on design and judgement instead.

**What does it run on?**
Windows 10/11 desktop. There is no web version.

---

## Data, privacy and export control

**Does my data leave my machine?**
No. There is no cloud backend, no accounts, no telemetry. Everything runs and
stays on your computer.

**Is it usable on ITAR/EAR-controlled programmes?**
It is designed for that case: local-only processing, no phone-home. **You remain
responsible** for classifying your data and controlling access to the machine,
backups, and any cloud-sync folder placement. See Compliance & Legal in the app.

**What about the AI features?**
Optional and **off by default**. The core pipeline is fully deterministic. If you
enable AI analysis it uses *your own* API key and sends excerpts to the provider
you configure — do not enable it for controlled data without approval from your
counsel or empowered official.

**Where is my data stored, and how do I remove it?**
In `%APPDATA%\pdr-generator\data`. **Compliance & Legal → Your Data & Privacy**
shows the exact path and offers **Erase all local data**, which overwrites files
before deleting them. Your licence is kept and your trial is not reset.
Uninstalling also offers to remove the folder.

**Is "erase" unrecoverable?**
Files are overwritten before deletion, which defeats normal recovery. On SSDs,
wear-levelling can retain copies beyond the reach of any application — for a
hardware guarantee, use full-disk encryption.

---

## Importing

**Which formats can I import?**
PowerPoint, Word, PDF, Excel/CSV, Markdown/text, Visio, images, and CAD
(.step/.stp, SolidWorks metadata). Multiple files at once; add more later and
regenerate — your manual edits are preserved.

**I imported my package and got zero requirements. Why?**
Almost always one of:
1. **You imported a previously generated PDR** instead of the source package.
2. **Your requirement IDs lack a separator** — `SYS 0101` isn't recognised,
   `SYS-0101` is.
3. **The requirement text has no modal verb** (`shall`/`should`/`will`/`must`).

See the [Formatting Guide](FORMATTING-GUIDE.md).

**I got requirements but no risks.**
Risk extraction needs a real **table**. Only PowerPoint and Excel preserve table
structure — a risk register inside a PDF is flat text. Export the register as
.xlsx and import it alongside.

**Does it handle my requirement numbering scheme?**
Most schemes: `SYS-0101`, `PL-1`, `ADC-3`, `PHX-3.01`, `REQ-001`,
`REQ-COMMS-01`, `SS_COMM_01`, `MAI-400`. It needs an uppercase prefix, a
dash/underscore, and digits. Standards references (`MIL-STD-1553`, `ISO-9001`,
`NPR-7123`, `TRL-9`) are deliberately excluded.

**One file failed to import — did I lose the others?**
No. Files are imported independently and failures are reported per-file.

---

## The Decisions tab

**Why is it empty?**
It needs an **allocation** to measure against — a statement like "dry mass shall
not exceed 240 kg". If your package states limits only in prose without units,
nothing is quantified. See the Formatting Guide, section 4.

**Why does it say my risks "cannot change a decision"?**
Because they aren't linked to anything they threaten. A risk with no traced
consequence can't move a design or an allocation — it's register content, not
decision content. Link them under **Link risks to allocations**.

**Why won't it estimate probabilities for me?**
Because a fabricated probability is worse than an honest gap. Probability and
consequence ranges are engineering judgement; the tool structures the
elicitation and does the maths, but the numbers are yours.

**What is ΔP(breach)?**
How many percentage points the probability of busting an allocation would drop if
that risk were fully retired. It's the number that separates a risk that changes
a decision from one that only changes the paperwork.

**Why does the cheap mitigation rank above the scary risk?**
Buy-down ranks by return — points of breach probability (or units of margin) per
$1,000. The largest risk is often not the best purchase.

**What is JCL?**
Joint Cost and Schedule Confidence Level. NPR 7120.5 expects NASA projects to
show 70% joint confidence. Funding cost at its own 70th percentile *and* schedule
at its own 70th percentile does **not** give 70% joint, because the same risks
drive both — the tool shows that gap explicitly. It needs cost and schedule
allocations plus risks carrying cost/schedule consequences.

**Is the JCL a formal NASA JCL?**
No. A formal JCL uses a cost-loaded schedule network with dependencies. This is
an honest estimate from the risks and targets in your package — useful for seeing
whether committed numbers are defensible, not a substitute for the full analysis.

---

## Licensing

**How does the trial work?**
14 days, full features, no account. The trial marker is stored outside the
erasable data folder, so clearing your data doesn't reset it.

**How do licences work?**
Offline license keys — no phone-home, no activation server. After purchase you
receive a key by email; paste it under **License**.

**Do I need internet?**
Only to download the installer and receive your key. The application itself
never requires a connection.

**Can I use it on more than one machine?**
Professional is a single-seat licence. Team covers unlimited seats at one
programme site. Contact us for multi-site or enterprise terms.

**Is it free for students?**
Yes — free for university CubeSat and capstone teams with .edu verification.

---

## Installation

**Windows says "Windows protected your PC".**
The installer isn't code-signed yet. Click **More info → Run anyway**. Verify the
SHA256 published on the release page if you want to confirm integrity.

**Where does it install?**
`%LOCALAPPDATA%\Programs\PDR Generator`. It's a per-user install and doesn't need
administrator rights.

**How do I uninstall?**
Windows Settings → Apps. The uninstaller asks whether to also delete your saved
data; choose No to keep projects for a future reinstall.

---

## Support

**support@embryospace.com** — questions, licence issues, bug reports.
Please include your version (shown in the installer filename) and, if reporting an
extraction problem, the file format you imported. **Do not send controlled or
proprietary material** without agreeing a handling arrangement first.
