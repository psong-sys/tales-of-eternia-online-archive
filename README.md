# Tales of Eternia Online Archive

A preservation-focused static archive for **Tales of Eternia Online**, Namco's discontinued MMORPG.

View the archive:

https://psong-sys.github.io/toeo-archive/

This site catalogs static client-side data recovered from the original game files: equipment IDs, enemy classes, NPC and monster sprites, battle-action timelines, minimaps, audio references, and decoded asset container formats.

## What This Is

This is a fan preservation and research archive. It documents what can be recovered from the original client files and presents that information in a browseable wiki-style format.

The archive focuses on static client data:

- Equipment and symbolic item IDs
- Enemy classes and behavior taxonomy
- NPC and monster sprite sheets
- Battle action and animation timeline records
- Zone and minimap references
- Audio filename catalogs
- Asset bundle registry data
- File-format notes for decoded client containers

## What This Is Not

This is not an official Namco project.

Gameplay values such as HP, levels, damage formulas, EXP, drop tables, quest logic, and most server-side rules were not stored in the static client assets. Those values were server-authoritative and are not part of this archive unless recovered separately.

## Site Contents

These are the main files and folders in this GitHub Pages build.

| Path | What it is |
| --- | --- |
| `index.html` | Main archive landing page with high-level counts, category links, and decoded container summary. |
| `about.html` | Explanation of what the archive can and cannot recover from the client. |
| `equipment/` | Equipment and avatar-part ID pages generated from `cid1.idt`, joined with available icon thumbnails. |
| `beasts/` | Enemy slot catalog, behavior taxonomy, and monster / named-entity sprite browser from `cid0.idt` and extracted sprite bundles. |
| `npcs/` | NPC sprite browser for the `NN` and `NM` families. |
| `actions/` | Battle-action timeline pages decoded from `btlact.dat` / TDAB records. |
| `zones/` | Zone and minimap reference pages built from extracted map/minimap metadata. |
| `bundles/` | Character/resource bundle registry from CRSD and resource-alias data from NNTB. |
| `static/` | Shared CSS, logo, icons, sprites, minimaps, and other static files used by the generated pages. |
| `build_wiki.py` | Static-site generator used to rebuild the HTML pages from extracted JSON and image data. |

## Reverse-Engineering Notes

The formats were identified by combining static reverse engineering with corpus checks against the original client data.

In broad terms:

- Container magic values such as `BNKD`, `IDTB`, `ICND`, `TDAB`, `CRSD`, and `NNTB` were located in the client binary and matched against files in the data corpus.
- Loader and validator functions were inspected in disassembly/decompiler tools, including Ghidra-style static analysis, to recover header fields, record strides, pointer relocation rules, and decryption/decompression call paths.
- Corpus probes were then written to verify those layouts across many files instead of relying on a single sample.
- Once a format was stable, small Python extractors converted the recovered data into JSON, PNGs, and generated HTML.

Not every file contains gameplay data. For example, many enemy-paired asset files turned out to be content-hash manifests for visuals rather than stat or drop tables. That negative result is part of the archive's value: it helps separate recoverable client structure from data that only existed on the live servers.

## Decoded Format Summary

| Format | What was recovered |
| --- | --- |
| BNKD | Texture/image bundle entries, including sprite sheets and icon/minimap graphics. |
| IDTB | Symbolic ID tables for equipment, enemies, NPCs, taxonomy labels, and related client identifiers. |
| ICND | Item icon registry and categorized 64x64 icon extraction. |
| TDAB | Battle action scripts: animation, sound, effect, movement, and frame-timeline records. |
| CRSD | Character/resource registry mapping IDs and symbolic names to `.atd` and `.cpd` resource files. |
| NNTB | Resource alias map showing which logical names share the same canonical asset bundle. |
| ATDT / PKDF / CPDT | Content-hash asset manifests. These were decoded as visual/resource references, not gameplay stat tables. |
| MAPI / MAPD | Minimap and map atlas references used by the zone pages. |

## Legal

All original game assets, names, logos, and related materials belong to their respective rights holders. This archive is provided for preservation, research, and documentation purposes only.

**Tales of Eternia Online** was developed/published by Namco / Namco Bandai and operated by ISAO Corporation.
