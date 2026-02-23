# Specification: Fix Documentation Links and Navigation

**Date:** 2026-02-22
**Scope:** Repair all broken links, update navigation, and correct version typos across the CE-QUAL-W2 site following the reorganization of documentation into `documentation/users-manual/` and `documentation/hab-modeling-users-manual/`.

---

## Background

The PDFs were moved from `documentation/` to `documentation/users-manual/`. The HAB user manual was created as markdown pages under `documentation/hab-modeling-users-manual/`. The old `hab-modeling.md` landing page in the site root has been deleted. These changes left broken links across multiple pages.

---

## Fix 1: Navigation — HAB Modeling link in `_config.yml`

**File:** `_config.yml` (line 29)

**Problem:** The nav entry `url: /hab-modeling/` pointed to the now-deleted `hab-modeling.md`. No page currently serves that URL.

**Solution:** Change the HAB user manual index permalink from `/hab-modeling/user-manual/` to `/hab-modeling/` so it becomes the HAB landing page directly, eliminating the need for a separate landing page.

**Changes:**

1. `_config.yml` line 29 — no change needed (nav URL `/hab-modeling/` stays as-is)
2. `documentation/hab-modeling-users-manual/index.md` line 4 — change permalink:
   - **Before:** `permalink: /hab-modeling/user-manual/`
   - **After:** `permalink: /hab-modeling/`

This cascading change affects the chapter page permalinks. Since each chapter page has its own explicit permalink under `/hab-modeling/user-manual/...`, those must also be updated:

3. `documentation/hab-modeling-users-manual/minimum-algae.md` line 4:
   - **Before:** `permalink: /hab-modeling/user-manual/minimum-algae/`
   - **After:** `permalink: /hab-modeling/minimum-algae/`

4. `documentation/hab-modeling-users-manual/low-do-mortality.md` line 4:
   - **Before:** `permalink: /hab-modeling/user-manual/low-do-mortality/`
   - **After:** `permalink: /hab-modeling/low-do-mortality/`

5. `documentation/hab-modeling-users-manual/algal-harvesting.md` line 4:
   - **Before:** `permalink: /hab-modeling/user-manual/algal-harvesting/`
   - **After:** `permalink: /hab-modeling/algal-harvesting/`

6. `documentation/hab-modeling-users-manual/nitrogen-fixation.md` line 4:
   - **Before:** `permalink: /hab-modeling/user-manual/nitrogen-fixation/`
   - **After:** `permalink: /hab-modeling/nitrogen-fixation/`

7. `documentation/hab-modeling-users-manual/quick-start.md` line 4:
   - **Before:** `permalink: /hab-modeling/user-manual/quick-start/`
   - **After:** `permalink: /hab-modeling/quick-start/`

---

## Fix 2: HAB manual index — broken chapter links

**File:** `documentation/hab-modeling-users-manual/index.md`

**Problem:** All chapter links use `../` prefix (e.g., `../minimum-algae/`). From the current permalink `/hab-modeling/user-manual/`, `../` resolves to `/hab-modeling/` — one level too high. After Fix 1 changes the index permalink to `/hab-modeling/`, the `../` prefix will resolve to `/` (site root), which is even more wrong.

**Solution:** Change all `../` relative links to `./` (or bare slug) so they resolve relative to the index page's permalink directory.

**Changes (all in `documentation/hab-modeling-users-manual/index.md`):**

| Line | Before | After |
|------|--------|-------|
| 24 | `(../minimum-algae/)` | `(minimum-algae/)` |
| 25 | `(../low-do-mortality/)` | `(low-do-mortality/)` |
| 26 | `(../algal-harvesting/)` | `(algal-harvesting/)` |
| 27 | `(../nitrogen-fixation/)` | `(nitrogen-fixation/)` |
| 28 | `(../quick-start/)` | `(quick-start/)` |
| 42 | `(../minimum-algae/)` | `(minimum-algae/)` |

---

## Fix 3: HAB chapter prev/next links

**Problem:** Each chapter page uses `../` for prev/next navigation. Currently with permalinks under `/hab-modeling/user-manual/X/`, `../` correctly resolves to sibling pages. After Fix 1 moves permalinks to `/hab-modeling/X/`, `../` from `/hab-modeling/minimum-algae/` resolves to `/` — broken.

**Solution:** Change prev/next links to use bare slugs relative to the parent.

**Changes:**

`minimum-algae.md` (line 44):
- **Before:** `[Previous: User Manual Overview](../) | [Next: Chapter 2 - Low DO Mortality](../low-do-mortality/)`
- **After:** `[Previous: User Manual Overview](/hab-modeling/) | [Next: Chapter 2 - Low DO Mortality](/hab-modeling/low-do-mortality/)`

`low-do-mortality.md` (line 54 in parameters table, line 104):
- **Before (line 54):** `(../minimum-algae/)`
- **After:** `(/hab-modeling/minimum-algae/)`
- **Before (line 104):** `[Previous: Chapter 1 - Minimum Algae](../minimum-algae/) | [Next: Chapter 3 - Algal Harvesting](../algal-harvesting/)`
- **After:** `[Previous: Chapter 1 - Minimum Algae](/hab-modeling/minimum-algae/) | [Next: Chapter 3 - Algal Harvesting](/hab-modeling/algal-harvesting/)`

`algal-harvesting.md` (line 133):
- **Before:** `[Previous: Chapter 2 - Low DO Mortality](../low-do-mortality/) | [Next: Chapter 4 - Nitrogen Fixation](../nitrogen-fixation/)`
- **After:** `[Previous: Chapter 2 - Low DO Mortality](/hab-modeling/low-do-mortality/) | [Next: Chapter 4 - Nitrogen Fixation](/hab-modeling/nitrogen-fixation/)`

`nitrogen-fixation.md` (line 66):
- **Before:** `[Previous: Chapter 3 - Algal Harvesting](../algal-harvesting/) | [Next: Quick Start Guide](../quick-start/)`
- **After:** `[Previous: Chapter 3 - Algal Harvesting](/hab-modeling/algal-harvesting/) | [Next: Quick Start Guide](/hab-modeling/quick-start/)`

`quick-start.md` (lines 36-39 table links, line 43):
- Change all `../X/` references to `/hab-modeling/X/`

---

## Fix 4: Downloads page — broken PDF links

**File:** `downloads/index.md` (lines 54-58)

**Problem:** PDF links point to old paths at `/documentation/W2manual45_Part*.pdf`. The PDFs now live at `/documentation/users-manual/W2manual45_Part*.pdf`.

**Changes:**

| Line | Before | After |
|------|--------|-------|
| 54 | `/documentation/W2manual45_Part1_Intro_rev9.pdf` | `/documentation/users-manual/W2manual45_Part1_Intro_rev9.pdf` |
| 55 | `/documentation/W2manual45_Part2_Theory_rev8.pdf` | `/documentation/users-manual/W2manual45_Part2_Theory_rev8.pdf` |
| 56 | `/documentation/W2manual45_Part3_InputOutputFiles_rev8.pdf` | `/documentation/users-manual/W2manual45_Part3_InputOutputFiles_rev8.pdf` |
| 57 | `/documentation/W2manual45_Part4_ModelExamples_rev3.pdf` | `/documentation/users-manual/W2manual45_Part4_ModelExamples_rev3.pdf` |
| 58 | `/documentation/W2manual45_Part5_ModelUtilities_rev9.pdf` | `/documentation/users-manual/W2manual45_Part5_ModelUtilities_rev9.pdf` |

---

## Fix 5: Downloads page — broken preprocessor link

**File:** `downloads/index.md` (line 41)

**Problem:** Links to `/executables/preW2-v45_64.exe` but the file is at `/executables/PSU_CE-QUAL-W2_v45_x64/preW2-v45_64.exe`.

**Change:**
- **Before:** `[preW2-v45_64.exe](/executables/preW2-v45_64.exe)`
- **After:** `[preW2-v45_64.exe](/executables/PSU_CE-QUAL-W2_v45_x64/preW2-v45_64.exe)`

---

## Fix 6: Downloads page — broken source code link

**File:** `downloads/index.md` (line 47)

**Problem:** Links to `/src/w2source_7_7_2025.zip` which does not exist. Actual files are:
- `ERDC_CE-QUAL-W2_source_v2026.02.zip`
- `PSU_CE-QUAL-W2_source_2025_07_07.zip`

**Change:** Replace the single source code row with two rows (one per version), matching the two-version structure used elsewhere on the page:

```markdown
| Item                             |                                                                                       |
| -------------------------------- | ------------------------------------------------------------------------------------- |
| CE-QUAL-W2 model (ERDC v2026)   | [ERDC_CE-QUAL-W2_source_v2026.02.zip](/src/ERDC_CE-QUAL-W2_source_v2026.02.zip)       |
| CE-QUAL-W2 model (PSU v4.5)     | [PSU_CE-QUAL-W2_source_2025_07_07.zip](/src/PSU_CE-QUAL-W2_source_2025_07_07.zip)     |
| CE-QUAL-W2 pre-processor         | [PreW2_source_July2025.zip](/src/PreW2_source_July2025.zip)                           |
```

---

## Fix 7: Downloads page — version number typos ("v2006" should be "v2026")

**File:** `downloads/index.md`

**Problem:** Three instances display "v2006" or "2006" where the intended version is "v2026" or "2026":

| Line | Before | After |
|------|--------|-------|
| 16 | `ERDC's CE-QUAL-W2 v2006 adds` | `ERDC's CE-QUAL-W2 v2026 adds` |
| 27 | `ERDC v2006` and `w2_v2006.02_win64.exe` | `ERDC v2026` and `w2_v2026.02_win64.exe` |
| 28 | `ERDC v2006` and `w2_v2006.02_linux` | `ERDC v2026` and `w2_v2026.02_linux` |
| 29 | `ERDC v2006` and `w2_v2006.02_macOS` | `ERDC v2026` and `w2_v2026.02_macOS` |
| 33 | `Version 2006` | `Version 2026` |

---

## Fix 8: Downloads page — HAB Modeling link to deleted page

**File:** `downloads/index.md` (line 19)

**Problem:** `[HAB Modeling](/hab-modeling/)` linked to the now-deleted `hab-modeling.md`. After Fix 1 remaps the HAB manual index to `/hab-modeling/`, this link will work again.

**Dependency:** Fix 1 must be applied. No additional change needed on this line.

---

## Fix 9: Documentation index — broken anchor links

**File:** `documentation/index.md` (lines 118-125)

**Problem:** Links to anchors that don't exist on their target pages:
- `/support/#faq` — support page has no `#faq` heading
- `/publications/#reports` — publications page has no `#reports` heading
- `/publications/#conferences` — publications page has no `#conferences` heading

**Solution:** Remove the anchors since those pages are stubs ("Under Construction"). Point to the base pages instead.

**Changes:**

| Line | Before | After |
|------|--------|-------|
| 119 | `[Frequently Asked Questions](/support/#faq)` | `[Frequently Asked Questions](/support/)` |
| 124 | `[Technical Reports](/publications/#reports)` | `[Technical Reports](/publications/)` |
| 125 | `[Conference Proceedings](/publications/#conferences)` | `[Conference Proceedings](/publications/)` |

---

## Fix 10: Exclude `design/` from Jekyll build

**File:** `_config.yml`

**Problem:** The `design/` folder contains internal specifications and should not be published to the site.

**Change:** Add `design` to the `exclude` list:

```yaml
exclude:
  - CLAUDE.md
  - Gemfile
  - Gemfile.lock
  - design
```

---

## Summary of files to modify

| File | Fixes |
|------|-------|
| `_config.yml` | Fix 10 |
| `documentation/hab-modeling-users-manual/index.md` | Fix 1, Fix 2 |
| `documentation/hab-modeling-users-manual/minimum-algae.md` | Fix 1, Fix 3 |
| `documentation/hab-modeling-users-manual/low-do-mortality.md` | Fix 1, Fix 3 |
| `documentation/hab-modeling-users-manual/algal-harvesting.md` | Fix 1, Fix 3 |
| `documentation/hab-modeling-users-manual/nitrogen-fixation.md` | Fix 1, Fix 3 |
| `documentation/hab-modeling-users-manual/quick-start.md` | Fix 1, Fix 3 |
| `downloads/index.md` | Fix 4, Fix 5, Fix 6, Fix 7 |
| `documentation/index.md` | Fix 9 |

**Total: 9 files, 10 fixes, ~40 individual line edits.**

---

## Implementation order

1. Fix 10 — exclude `design/` from build (prevents spec from being published)
2. Fix 1 — update all HAB manual permalinks (foundation for all other HAB link fixes)
3. Fix 2 — fix HAB manual index chapter links
4. Fix 3 — fix HAB chapter prev/next links
5. Fix 4 — fix downloads page PDF links
6. Fix 5 — fix downloads page preprocessor link
7. Fix 6 — fix downloads page source code link
8. Fix 7 — fix downloads page version typos
9. Fix 9 — fix documentation index broken anchors

Fix 8 resolves automatically once Fix 1 is applied.
