# Changelog

## 7.12.0 — 2026-10-28

- Add native `--match scamp` as a separate initial strategy; retain pair as default and leave triangle available without hidden fallback between methods.
- Recover scale/rotation from FFT correlations of unit-weight log-separation/undirected-angle pair histograms, then recover translation with positional FFT correlations. Handle linear versus periodic axes explicitly, both 180° branches, sub-bin peak refinement and independent competing-peak contrast.
- Project all fetched references on a local TAN matching plane while preserving celestial frame, axes and resolved scale. Reuse existing detection, providers, flips, unique rematching, similarity refinement, TAN/SIP fitting, clipping and held-out validation. Preserve explicit radii and instrument presets.
- Reject ambiguous SCAMP seed identities using symmetric full-list neighbour checks after similarity refinement.
- Expose bounded source/reference caps; document QAC-specific binning, filtering, weighting and contrast diagnostics. Add independent stage/integration tests and a controlled benchmark using identical frozen inputs. This compatible strategy adds no dependency and increases the minor version.

## 7.11.0 — 2026-10-27

- Add `--match pair|triangle`, retaining pair matching as the default and selecting triangle-based initial correspondences explicitly.
- Index normalized side-length ratios from local and bright-star triangles, bound candidate searches, reject degenerate triangles, and verify transformations against the wider star list. Triangle mode does not silently fall back to pair matching.
- Reuse the existing similarity refinement, unique rematching, magnitude groups, flip modes, TAN/SIP fits, clipping and held-out validation. Preserve shifted windows, explicit radii, and stellar FWHM retries. Add deterministic offline checks and concise documentation; comparative observational benchmarks remain deferred.
- This compatible optional matching method increases the minor version and adds no dependency.

## 7.10.1 — 2026-10-27

- Share the normal reference-window margin and boundaries between star selection and shifted-search coverage.
- Consolidate catalogue query calls while preserving per-depth cache state; express wider-retry eligibility explicitly and reuse PS1 magnitude defaults.
- Shorten the README, clarify pixel-scale tolerance and window margins, and prefer the correctly spelled `--distortion` while retaining its legacy alias. This maintenance patch makes no intended astrometric or CLI behaviour changes.

## 7.10.0 — 2026-10-27

- Add opt-in `--bad-pointing`, with explicit alias `--bad`, to try the original centre followed by north, east, south, and west centres displaced by half the shorter field side. Stop at the first solution accepted by the existing fitting and validation rules; retain the original reference-selection window.
- Reuse one original-centred catalogue pool per attempted magnitude depth across trial centres, together with detected sources and the stellar FWHM estimate. Automatic sizing covers all five usual reference windows, including their 30% margins, for every catalogue provider. Preserve the normal mode's existing instrument, wider-radius, and depth behavior.
- Keep an explicit `-r` as the exact original-centred bounding cone, without automatic enlargement or shifted-centre catalogue queries. Document its possible coverage limitation. Keep pointing-offset diagnostics tied to the original explicit `-c` coordinates.
- Update help, portable documentation, and regression coverage. This compatible opt-in recovery feature increases the minor version.

## 7.9.0 — 2026-10-26

- Make the existing image-based stellar FWHM estimate the default for QAC commands. Bare `--fwhm` selects the same mode; numeric `--fwhm PIXELS` remains fixed.
- Keep the established 3- then 6-pixel detection and matching retries when estimation is unavailable or its match fails. Add `--nofwhm` to request that historical retry directly.
- Clarify the pilot's 3-to-6-pixel control label without changing recorded historical results. Update CLI help, portable documentation, and offline regression tests. The compatible default-workflow change increases the minor version.

## 7.8.0 — 2026-10-26

- Accept bare `--fwhm` to estimate a rough stellar FWHM in image pixels from isolated, round, high-significance sources using Photutils segmentation and second moments. It requires no angular pixel scale or `CLASS_STAR` classifier.
- Try the image-derived value before the existing 3- and 6-pixel guesses. If too few suitable sources are found, retain the existing retries; a numeric `--fwhm PIXELS` remains fixed.
- Reuse the detector's background and noise calculation for estimation, report the estimate and selected source count, and add synthetic, offline solve, and fallback checks in Python 3.10 and 3.12. This compatible option mode increases the minor version.

## 7.7.0 — 2026-10-26

- Automatically retry source detection and astrometric matching with a 6-pixel stellar FWHM guess when the default 3-pixel guess finds too few stars or cannot match them. Keep a supplied `--fwhm` fixed.
- Detect the broader profile before catalogue access when 3 pixels finds too few stars. Reuse the fetched catalogue when the initial match fails, and reuse detections across Gaia depth and wider-radius retries.
- Keep the pointing-pilot observer's timed detection adapter compatible with both FWHM guesses and cache each result across trial centres. Historical benchmark results are unchanged.
- Report the successful FWHM guess and retain its detected sources in plots and diagnostics. Add synthetic broad-star and match-failure regression tests. This compatible automatic workflow increases the minor version.

## 7.6.1 — 2026-10-26

- Accept MAST GSC CSV responses whose first line contains only `#Objects found : N`, as observed in a live GSC 3.3 query. Keep explicit wrong-release and malformed-response rejection.
- Correct the GSC response fixture and documentation. This is a compatible bug fix, so the patch version increases.

## 7.6.0 — 2026-10-26

- Add GSC 3.3 as `-s gsc` or `-s gsc3.3`, using MAST's versioned cone-search API and keeping Gaia DR3 as the default catalogue.
- Select classified stellar rows using GSC's native `mag` with a default 12–20 range. Accept `-m` and observation-date propagation through MAST; reject non-GSC33 responses, malformed replies, and queries at the 10,000-row cap.
- Update CLI help, README, and offline provider/integration tests. This compatible catalogue addition increases the minor version.

## 7.5.0 — 2026-10-26

- Add `--fwhm PIXELS` to set the approximate stellar profile width for source detection while retaining the 3-pixel default. Accept finite positive widths, including 1.5, 2, and 7 pixels; reject invalid values before reading the image.
- Keep pixel scale, catalogue selection, matching, and output behavior unchanged. The new optional detection control is a compatible feature, so the minor version increases.

## 7.4.0 — 2026-10-26

- Add AllWISE (`allwise`, `aw`) and UCAC5 (`ucac5`, `uc`) reference catalogues through VizieR. Keep Gaia DR3 as the default and preserve existing aliases and local-catalogue handling.
- Default to AllWISE W1 with 8 ≤ W1 < 16 and UCAC5 G with 8 ≤ G < 16. Support W1–W4 and G/R/J/H/Ks selection, catalogue-specific bright/faint defaults, and explicit magnitude ranges.
- Select clean, unblended AllWISE stationary positions using catalogue quality, saturation, and positional-error fields; do not interpret its apparent motions as proper motions.
- Use UCAC5's Gaia-epoch J2015.0 positions and genuine proper motions at the image observation date, with explicit behavior for missing dates, unusable motions, and missing-photometry placeholders. Key propagated-reference reuse by observation date.
- Reuse VizieR transport/cap checks for 2MASS and the new providers, and the existing Gaia angular-motion calculation for UCAC5. Preserve existing fitting, validation, and output behavior; AllWISE initial matching considers up to 200 detections.
- Update CLI help, portable examples, catalogue-quality limitations, and deterministic provider/integration tests. This compatible catalogue expansion increases the minor version.

## 7.3.0 — 2026-10-24

- Restore `Pointing offset: X.x″` above the concise `X% of shorter side` line, retaining orange underlining above 5%, diamonds, and north-up/east-left `-q` views.
- Make `-p/--plot` try opening every published diagnostic PNG in the system default viewer, including pages from partial results. Reuse the finding-chart tool's detached Linux/macOS launch pattern and support the Windows file handler.
- Launch only after the full output bundle is saved; missing launchers and launch errors leave saved files and calibration exit codes intact. Update CLI help and documentation.
- This compatible viewer workflow addition increases the minor version.

## 7.2.0 — 2026-10-24

- Orient successful explicit `-q` diagnostic fields north up and east left, including selected single frames and paginated views. Use a centred TAN display projection enclosing the calibrated footprint; retain native pixel axes for failures.
- Map accepted stars and annotations onto the display grid without changing FITS pixels, calibrated WCS, residual statistics, or original-field offset percentages.
- Replace the requested-coordinate cross with an open orange diamond, remove the centre cross, and simplify the label to `X% of shorter side`. Retain orange underlining above 5% and request-to-centre arrows.
- This compatible plotting enhancement increases the minor version.

## 7.1.0 — 2026-10-24

- Report explicit `-c` coordinates' angular separation from each successfully calibrated output-image centre, with and without diagnostic PNGs.
- Add orange requested-position and centre markers and a request-to-centre arrow to single and combined diagnostic fields. Clip off-field arrows to the panel edge and identify off-field requests.
- Show the offset in arcseconds and as a percentage of the shorter angular field span; underline its text in orange above 5%. Measure spans from opposite edge midpoints using the output WCS, including SIP and resampled outputs.
- Reuse successful-frame diagnostics and the shared field renderer. Omit annotations for failed frames and when no explicit `-c` was given.
- This is a compatible feature addition, so the minor version increases.

## 7.0.0 — 2026-10-24

- Attempt every selected image frame after expected calibration or resampling failures. Save a partial result when at least one frame succeeds; retain failed input pixels and unverified input WCS.
- Add selected-frame `QACSTAT`, `QACERR`, `QACVER`, and `QACRSMP` metadata plus primary `QACRUN`, `QACNSEL`, `QACNSOL`, and `QACNFAI` run summaries. Clear stale failure messages on successful frames.
- Return exit code 0 for complete success, 1 for a saved partial result, and 2 for no successful frames or handled fatal errors. A partial run prints its solved/selected counts.
- Highlight failed panels and table rows in red, use pixel axes for them, show failure reasons, and exclude failures from residual/RMS statistics. Handle failed-only pages and invalid/constant image displays.
- Compact the contact sheet, move the key to the header, reserve red for failures, and show MODS's four quadrants beside an enlarged MERGED view instead of leaving a legend-sized empty tile.
- This is a major release because multi-frame failure behavior changes from rejecting the whole result to writing successful calibrations with explicit partial status and exit code 1.

## 6.0.0 — 2026-10-24

- Combine selected frames into one diagnostic PNG with a field grid, shared star-marker key, colour-coded per-frame counts/RMS/validation/scale table, shared angular residual scatter, and per-frame fit/validation RMS comparison.
- Reuse the existing field renderer, output-grid transformations, accepted matches, and validation statistics. Preserve individual-frame rendering for single-frame selections, independent WCS fits, and FITS pixel/output behavior.
- Paginate selections exceeding six frames with stable original frame numbers and complete output collision checks before solving.
- This is a major release because multi-frame PNG output names change from individual `_qN.png` files to `OUTPUT.png` or `OUTPUT_pageN.png`.
- Correct the documented standard-library unittest command's pattern option.

## 5.0.0 — 2026-10-24

- Make every `-i` instrument preset override header WCS scales and `PIXSCALE`/`SECPIX` values, consistently across all selected frames and `-q` runs.
- Keep explicit `-ps` highest in priority. Preserve binning adjustments for presets, header orientation/pointing, BFOSC's default virtual Y flip, and scale refinement from matched stars.
- Centralize the priority rule in WCS initialization and remove the BFOSC-only scale override from the solve loop.
- This is a major release because existing commands combining `-i` with header scales now use the selected instrument scale instead of the header scale.

## 4.0.0 — 2026-10-24

- Reassign `-p` to `--plot`; pixel scale uses `-ps`, `--pixel-scale`, or `--scale`. Update CLI guidance, examples, and tests consistently. This is incompatible with commands using `-p SCALE`.
- Display diagnostic fields with black stars on a light sky, sampled percentile and sigma-clipped auto cuts, and an asinh stretch of 0.08 targeting an approximately 75% white background.
- Fill the diagnostic page more effectively with the summary above adjacent residual graphs, larger fonts and legends, and outlined markers and compass annotations.
- Keep all detector pixels, fitted matches, WCS fitting, and per-frame output selection unchanged.

## 3.1.0 — 2026-10-24

- Accept `ps` as a short alias for the PS1 catalogue.
- Add optional `--plot` PNG diagnostics for each solved frame, with cyan final-match rings, larger gold rings for the ten brightest detected sources, a legend, N/E arrows, and an angular scale bar.
- Show signed East/North residual scatter, enlarged spatial residual vectors, fit and held-out refit RMS, match counts, residual percentiles and offsets, catalogue/model information, pixel scale, and observation time.
- Reuse the exact accepted correspondences and existing TAN/SIP validation; transform markers onto the actual output grid for resampled images.
- Add Matplotlib as a plotting dependency, use headless rendering, and stage FITS and PNG outputs before publication with existing-file protection.
- Include the offline regression suite in the current tests directory and check automatic reflections by sky mapping while accepting equivalent X/Y orientation labels.

## 3.0.1

- Clarify accepted reference-source names in `--help` without adding aliases.
- Stage solved FITS output beside its destination and publish only after the full write succeeds.
- Keep the existing no-replacement default, including if another file appears while solving.

## 3.0.0 — 2026-10-24

- Change `-s` from pixel scale to reference survey; `-s`, `--survey`, and `--catalog` now select the same source.
- Add `-p`, `-ps`, and `--pixel-scale` for the image scale in arcseconds per pixel; retain `--scale`.
- Add `-v` as an alias for `--version` and update scale guidance in CLI messages and documentation.
- This is a major release because existing commands using `-s` for scale need `-p` or `--scale`.

## 2.0.0 — 2026-10-19

- Add `-r ARCMIN` / `--radius ARCMIN` to set the catalogue cone radius for Gaia, PS1, 2MASS, and local-catalogue filtering. Values must be finite and positive.
- An explicit radius overrides automatic sizing and disables wider-radius retries. Without it, existing automatic sizing and retries remain unchanged.
- Breaking CLI change: `-r` now requires a radius and no longer enables resampling. Use `--resample` to retain the previous resampling behavior, including its implicit degree-2 SIP fit unless another supported degree is specified.
- Update CLI help, portable README examples, and regression tests.

The previous release was 0.5.11. Version 2.0.0 is the requested major release for this incompatible CLI change.
