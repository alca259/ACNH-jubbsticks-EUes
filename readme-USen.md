# ACNH EUes Fan Translation (English Overview)

This document explains the repository structure and workflow for the European Spanish (EUes) fan translation of *Animal Crossing: New Horizons*. It mirrors the Spanish `readme.md` so non‑Spanish contributors or observers can understand what is going on without reading Spanish.

## Goal
Provide fully translated, structurally correct MSBT text resources for the game in European (Peninsular) Spanish while keeping strict parity with the original US English data set (`USen/`).

## High-Level Folder Map

### Root
- `Gyroid_list.txt` – Canon / approved gyroid name mapping list (used to keep gyroid item naming consistent).
- `List of new labels by file.txt` – Manual log of any newly added or discovered MSBT labels to track progress.
- `readme.md` – Main (Spanish) README.
- `readme-USen.md` – This English helper document.

### `EUes/`
Editable translation sources (UTF‑8 with BOM `.msbt.txt`). Structure must mirror `USen/` exactly. Subfolders:
- `LayoutMsg/` – Layout / version meta message(s).
- `Mail/` – In‑game mail templates (Mother, special NPC letters, etc.).
- `String/` – Core string tables: item names, fish, bugs, shells, plants, crafting materials, customization (color / fabric / part) names and variant prefixes (`C#`, `F#`, `X`).
- `System/` – UI text, Nook Miles achievement text, passport descriptors, general system prompts.
- `TalkFtr/` – Dialogue tied to furniture / interactable features (e.g. workbench messages).
- `TalkNNpc/` – Normal villager dialogues (different personalities; gift selection etc.).
- `TalkObj/` – Dialogues for special interactable objects that are not standard NPCs.
- `TalkSNpc/` – Special NPC dialogue (e.g. Blathers, Brewster, K.K. Slider, etc.).
- `TalkSys/` – System / player-facing dialogue (bulletin board, notifications, etc.).

### `USen/`
Reference English source tree. Do **not** edit. Used only for context, meaning and ensuring 1:1 label parity.

### `romfs/`
Binary output area for distribution / mod injection.
- `Message/` – Compressed `.sarc.zs` archives per category (generated from `EUes/` text files).
- `System/Resource/` – Additional system resource files (usually untouched here). May include the `resourcetablesize` file (see DLC section below).

## Workflow (Simplified)
1. Edit only inside `EUes/`.
2. Keep structure synchronized with `USen/` (add missing counterpart files when they appear upstream).
3. Repack to `.sarc.zs` archives in `romfs/Message/` using external packaging tooling (not stored here).
4. Log any brand‑new labels in `List of new labels by file.txt`.

## Key Translation / Editing Rules
- Never change `label` values or remove the `---` delimiters around entries.
- Preserve all markup tags exactly (anything inside `{{ ... }}`) such as `{{wordInfo ...}}`, `{{anim:...}}`, `{{color ...}}`, `{{pageBreak}}`, `{{delay8}}`.
- Do not translate or alter tag attribute names or ordering.
- Maximum visible line length: 90 characters (excluding embedded markup tags). Exception: lines split by `{{pageBreak}}` restart the count after the break tag.
- Follow Peninsular Spanish norms (gender, articles) controlled partly by `{{wordInfo}}` attributes.
- Use established proper noun mappings (e.g. Brewster → Fígaro, Blathers → Sócrates) and gyroid names from `Gyroid_list.txt` (e.g. brewstoid → figaroide).

## Special Prefix Logic (Item Names)
- `C#` prefix: Color customization variants (e.g. `C8` = 8 color options).
- `F#` prefix: Fabric customization variants.
- `X` prefix: Indicates there is also a plural variant with `_pl` suffix.

## DLC Compatibility: `resourcetablesize`
The mod/base that enables loading the Happy Home Paradise DLC normally ships with a `resourcetablesize` file tailored to officially supported languages. That version is **not** compatible with this custom `EUes` translation. To allow the Spanish fan translation to load, an empty replacement file is included/expected instead, which disables proper DLC integration.

Trade‑off:
- Original DLC `resourcetablesize`: DLC features work, but breaks custom Spanish language pack.
- Empty placeholder: Custom Spanish works, DLC feature integration is lost.

A full solution would require rebuilding `resourcetablesize` merging the resource index entries for both the DLC and the new language pack. (Not implemented here.)

## Quality / Consistency Notes
- Any broken or malformed tag will cause packing failures or in‑game rendering issues.
- Keep terminology consistent across categories; item names in `String/` should exactly match references in dialogue files.

## Contributing (English Speaker Guidance)
If you do not speak Spanish but want to help:
- Focus on structural parity: ensure all labels present in `USen/` exist in `EUes/`.
- Leave untranslated strings flagged for review instead of guessing (do NOT rename labels).
- Report any new labels you spot into `List of new labels by file.txt`.

## Future Improvements (Open)
- Automated validation script for tag integrity and line length.
- Reconstructed `resourcetablesize` enabling DLC + custom language simultaneously.
- Terminology glossary extractor / consistency checker.

---
For questions, open an issue or refer to the Spanish `readme.md` for deeper linguistic guidance.
