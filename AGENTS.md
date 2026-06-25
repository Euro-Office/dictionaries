# dictionaries — Euro-Office Spellchecking Assets

@../AGENTS.md

Guidance for Claude Code (and other AI agents) working in **dictionaries** — Hunspell-compatible assets for multilinguistic spellchecking.

## What this repo is
A static, non-compiled data store holding language rules, affix matrices, and vocabulary databases for 45+ locales, consumed directly by the `server/SpellChecker` binary wrapper.

## Data Schema & Character Encoding Constraints
- **Hunspell Architecture:** Every locale contains two essential files: `<locale>.dic` (word list) and `<locale>.aff` (affix definitions). They must remain structurally consistent with standard Hunspell specifications.
- **Line Ending Enforcement:** **CRITICAL FAIL MODE.** The parser expects strict LF line endings. Running an AI agent on a Windows host that silently updates file changes to CRLF will break the SpellChecker parsing offsets, causing silent engine crashes or complete breakdown of spellchecking for that specific locale.
- **Character Encoding:** Files must adhere strictly to the character encoding declared in the first line of the `.aff` file (typically `SET UTF-8`). Mixing encodings within the dictionary file will corrupt word lookup tables.

## Rules
- **Never** introduce any custom automation code, node packages, or shell wrappers here. This repository is legally restricted and optimized as a static asset container.
- **Never** remove original open-source attribution headers (Hunspell/GNU/LGPL licenses) from the individual locale folders; doing so breaks software compliance rules.
- **Always** ensure that adding or expanding word lists passes character validation to avoid breaking byte-count-based dictionary lookups.

## Findings & Long-tail
No centralized findings store exists in this repository yet. Document edge cases in code comments or GitHub issues until one is established.