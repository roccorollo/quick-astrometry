# Changelog

## 9.2.4 — 2026-10-30

- Restore the single-frame right column to a readable statistics block above side-by-side residual scatter and vector graphs. Preserve the left-aligned field, fonts, measurements and combined layouts.

## 9.2.3 — 2026-10-30

- Left-align the single-frame diagnostic field and reserve a horizontal gap before the solution header, preventing contact between the image and upper-right text. Keep image aspect ratio, fonts and combined layouts unchanged.

## 9.2.2 — 2026-10-30

- Preserve grid selection and priority from source-analysis pixels through original-pixel fitting and diagnostics, fixing cell reassignment near boundaries after binning.
- Reuse the existing per-FWHM source cache for spatial priority across catalogue, radius, window and matcher retries. Remove grid rebuilding and diagnostic index remapping; non-grid selection is unchanged.
## 9.2.1 — 2026-10-30

- Remove the ten-brightest-source gold circles and their legend entries from single-frame and combined diagnostic plots. Keep cyan final-fit markers; brightness is not a measure of a star's influence on the match. Matching and grid selection are unchanged.

## 9.2.0 — 2026-10-30

- Add `-nd/--number-detections` to override the initial-matching detection budget, increasing the retained source limit above 200 when necessary. Existing catalogue defaults and reference brightness groups remain unchanged.
- Add opt-in `--grid [N]` spatial detection selection (2–19 cells per side; bare: 3), reused through matching and refinement, with unused sparse-cell places redistributed. Allow `--bad` together with an uppercase warning that the combination is not tested.

## 9.1.0 — 2026-10-30

- Group `--resample` beside `-d/--distortion/--distorsion` in CLI help and documentation, without changing their behaviour.
- Expose Pan-STARRS as the primary public survey name (`-s pan-starrs`, case insensitive), retaining `ps` and legacy `ps1` aliases. Update help, query messages, catalogue/plot labels and current documentation.
- Reuse the existing Pan-STARRS1 DR2 provider, magnitude defaults, quality cuts and API without changing matching budgets or scientific calculations. This compatible survey-name addition increases the minor version.

## 9.0.0 — 2026-10-30

- Make `--match auto` the default: exhaust pair matching across the normal workflow and permitted wider cone, or all five bad-pointing windows, before restarting the same workflow with triangle. Stop at the first accepted window solution and retain explicit pair-only and triangle-only modes.
- Reuse per-FWHM detections and exact radius/depth catalogue pools across methods, restoring Gaia depth metadata. Keep original pointing, explicit radii, instrument settings, scientific fitting and validation unchanged; catalogue outages do not trigger algorithm fallback.
- Remove SCAMP and its controls from the public CLI while preserving its internal implementation, configuration, tests and benchmark records. This incompatible CLI removal requires a major version.
- Add deterministic recovery-order, cache, restart and outage checks; report the accepted matcher in terminal summaries. Grid-based source selection remains deferred.
- Pin the existing pointing-comparison Observer adapter to pair-only matching so its reference-policy experiments do not silently gain the new automatic strategy. Preserve recorded benchmark results.

## 8.2.3 — 2026-10-30

- Increase the triangle matcher's global bright-star subset from 24 to 25 stars. Keep local-neighbour triangles, candidate limits, pair matching and validation unchanged. This compatible seed-budget adjustment increases the patch version.

## 8.2.2 — 2026-10-29

- Change the last fallback stellar FWHM guess from 30 to 35 original-image pixels; use the shared 5/15/35 sequence in help, messages and all fallback paths.
- When automatic elongation has insufficient suitable candidates, report its unavailability and continue with default shape handling instead of failing the frame. Preserve the twelve-candidate guard for learning a band and the independent FWHM-estimation requirements.
- Reuse the default detection/FWHM path, including 5/15/35 original-pixel retries, fixed FWHM and `--nofwhm`. Preserve explicit numeric elongation settings and genuine image/background errors. This compatible recovery fix increases the patch version.

## 8.2.1 — 2026-10-29

- Treat SIFAPSOFT binning 4 and automatic elongation as defaults: explicit options override each independently, regardless of argument order. Preserve bare-option semantics and explicit programmatic values across repeated frame solves. This compatible precedence correction increases the patch version.

## 8.2.0 — 2026-10-29

- Make `-i sifapsoft` always select analysis binning 4 and automatic elongation, overriding other valid analysis values consistently in CLI and programmatic frame solves. Keep camera-scale handling, other instruments, source-area criteria and FWHM fallback guesses unchanged. This compatible instrument workflow change increases the minor version.

## 8.1.2 — 2026-10-29

- Extend fallback stellar FWHM guesses to 5, 15 and 30 original-image pixels, in that order. Reuse the same sequence after automatic-estimation or matching failure and with `--nofwhm`; preserve early success, binning conversion, detection caching and explicit fixed FWHM.
- Derive terminal/help wording from the configured sequence and update documentation and retry regression checks. This compatible fallback adjustment increases the patch version.

## 8.1.1 — 2026-10-29

- Clarify the assumed camera-binning message for input images, preserving each instrument's preset value and all binning calculations. This output-wording correction increases the patch version.

## 8.1.0 — 2026-10-29

- Add `--elongation [MAX]`: preserve the default 1.3 FWHM cutoff, accept a numeric maximum, or learn a median/MAD band with a bare option. Require twelve bright, isolated, size-consistent candidates; use three robust scatters with a five-percent relative tolerance floor and report the measured band. Shape consistency is not stellar classification.
- Share the candidate map and selection across FWHM fitting and detection retries, including fixed FWHM and `--nofwhm`. For nondefault shape modes, reuse moment covariance to fit rotated elongated profiles, replace DAO roundness gates with measured axis-ratio selection, and retain one DAO centre per segmented object. Preserve other quality, matching and WCS checks.
- Make detection binning 2 the default and the bare `--binning` value. Retain explicit factors, including `--binning 1` for native analysis, original-pixel FWHM/scale semantics and unchanged output samples. This compatible configurable workflow and requested default change increase the minor version.
- Keep Observer diagnostics in original-pixel FWHM units and record the solver's shared analysis-binning default. Update synthetic recovery fixtures to retain suitable isolated stars after averaging; preserve historical observations and recorded runs.
- Document statistical assumptions and sampling limitations; test robust selection, sparse/zero-scatter cases, rotated profiles, shape outliers, CLI modes and offline native-grid astrometry in both supported Python environments.

## 8.0.1 — 2026-10-29

- Select FWHM candidates directly from cached region areas after one segmentation. Preserve the adaptive area formula, candidate footprints and all original regions as possible neighbours and fitting masks.
- Remove the redundant second segmentation, flux-weighted cross-map association helper and unused ambiguous-region bookkeeping. Keep profile fitting, elongation restrictions, CLI behaviour and astrometric validation unchanged. This compatible performance correction increases the patch version.
- Verify native/binned candidate-footprint equivalence against repeated segmentation, including small neighbours and masked pixels.

## 8.0.0 — 2026-10-29

- Remove `--smooth` and all Gaussian preprocessing/verification filters. Use one source-analysis procedure on native or explicitly binned pixels; retain DAOStarFinder and Gaussian profile modelling. Removing the CLI option is an incompatible change and requires a major version.
- Target 256-pixel background meshes, retaining smaller meshes for small working images. Estimate a robust rough width population, adapt candidate region area in one additional segmentation at most, and retain small regions as neighbours. Preserve the 80% positive-signal association criterion without an auxiliary filtered image.
- Simplify profile fitting from nine nonlinear parameters to six: estimate a clipped local sky plane separately and use an analytical Gaussian Jacobian. Share bounded cutout enlargement, fit-area and final-width isolation checks; retain the twelve-profile minimum and 80-candidate cap.
- Replace the 40-pixel width cutoff with an image-derived range and a 100-working-pixel safety limit, update Gaussian sigma bounds consistently, and reject fits pinned to those bounds. Preserve original-pixel FWHM reporting, explicit FWHM, 5/15 retries, original FITS samples, instrument presets and astrometric strategies.
- Replace smoothing-specific tests and documentation with shared native/binned source-analysis coverage. No new dependencies.

## 7.16.0 — 2026-10-29

- Add opt-in `--smooth [SIGMA]` Gaussian source analysis with unchanged image dimensions and original-pixel units; default sigma 1, alternative to detection binning. Fit profiles and preserve FITS pixels on the unfiltered image, correcting only the detection kernel for Gaussian blur.
- Select larger image-dependent region areas in bounded trials using filter size and coarse stellar width. Group fragments supported by a coherent 2×2 auxiliary map, preserve ambiguous regions and faint auxiliary objects as possible neighbours, and reject multi-peaked width candidates.
- Share cleaned labels with fitting masks and cutout limits, recheck isolation after fitting, and allow one bounded cutout enlargement with a valid-area check against `int(FWHM + 1)²`. Raise the automatic fitted-width ceiling from 30 to 40 working pixels as requested. Preserve 5/15 retries, explicit FWHM, matching strategies and WCS validation.
- Document empirical choices and limitations, and add deterministic smoothing, blend, masking, area-adaptation and original-grid FITS/WCS checks. This compatible opt-in workflow increases the minor version without adding dependencies.

## 7.15.1 — 2026-10-29

- Change automatic fallback stellar FWHM trials, including `--nofwhm`, from 3/6 to 5/15 original-image pixels. Preserve the estimated width as the first attempt, explicit fixed widths, binning conversion and detection-cache reuse. Centralize the retry pair and update help and regression tests. This compatible fallback adjustment increases the patch version.

## 7.15.0 — 2026-10-29

- Replace threshold-truncated moment widths with robust elliptical-Gaussian fits in larger original-data cutouts, fitting a local sky plane and estimating local background scatter. Use segmentation only for candidate positions, initial sizes and neighbour masks; include sub-threshold wings in the fit.
- Bound fitting to 80 bright candidates, reject unstable/poor profiles, and retain the final 1.5–30 working-pixel width, elongation <1.3, bright-source and twelve-profile requirements. Allow initial moment widths down to 1 pixel so truncation need not exclude a valid fitted width.
- Distinguish bright-candidate peak selection (15 times background scatter) from fitted Gaussian peak contrast (at least 5 times local scatter), with independent shape, convergence and residual checks; neither is a formal integrated-source signal-to-noise estimate.
- Reuse existing binning, original-pixel conversion, detection and WCS validation. Preserve explicit `--fwhm`, `--nofwhm` and the 3/6-pixel retries. This compatible estimation workflow change increases the minor version without adding dependencies.

## 7.14.2 — 2026-10-29

- Split plot headers into left-aligned image information and right-aligned solution metadata. Compact single-frame summaries, enlarge the field area and stack residual graphs vertically.
- Move shared multi-frame metadata above the quality table, giving graphs more space while preserving per-frame centre/FOV labels, independent statistics and failure indicators. Retain the established font family and three sizes. This compatible layout correction increases the patch version.

## 7.14.1 — 2026-10-29

- Reduce the QAC plot heading and enlarge the filename/HDU and centre/FOV lines with clearer header spacing. Match centre/FOV text to the solution-summary size.
- Standardize single- and multi-frame plots on DejaVu Sans at 9, 13 and 15 points, including axes, legends, tables and annotations. This compatible presentation correction increases the patch version.

## 7.14.0 — 2026-10-29

- Report `Image Center` in HMS/DMS and width × height FOV in terminal output and single-/multi-frame diagnostic plots. Use one decimal place and arcseconds below 1 arcmin on both sides, degrees above 50 arcmin on both sides, otherwise arcminutes.
- Reuse the existing edge-midpoint geometry for pointing statistics and reports. Measure the solved output grid before diagnostic rotation/padding, including resampled outputs; do not label failed frames as calibrated. This compatible reporting feature increases the minor version.

## 7.13.0 — 2026-10-29

- Add opt-in `--binning FACTOR` block averaging for detection and stellar FWHM estimation; default 1 preserves existing behavior. Reuse existing background estimation, shape restrictions, detection, matching and WCS validation.
- Map centroids back to original block centres and retain original-pixel scale/FWHM semantics, image geometry and FITS pixels. Exclude incomplete bottom/right blocks from detection and preserve invalid blocks. This compatible feature increases the minor version without adding dependencies.

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
