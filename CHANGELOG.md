# Changelog

All notable changes to this project are documented in this file.

## 4.1 - 2024-05-29
- Require Java 11+
- DDA+ mode supports ddaPASEF data
- Significantly faster loading of Thermo raw files
- Calculate and report more modification-related scores for PSMs identified in open and mass-offset search workflows (especially useful for chemoproteomics workflows). The following columns added to PSM.tsv files: 
    - `ptm_mass`: mass of the modification
    - `localization_peptide`: a peptide string with lowercase amino acids to indicate the sites with the best score
    - `best_positions`: a list of sites with the best score in the format `<amino acid 1><site index 1>:<amino acid 1><site index 1>:...`. For example `T(4)I(5)`.
    - `number_best_positions`: number of the sites with the best score
    - `score_all_unshifted`: the score when matching only unshifted fragments (unshifted fragment is a fragment not containing any modification mass)
    - `score_best_position`: the score when putting the modification on the best (i.e. higest scoring) site
    - `score_second_best_position`: the score when putting the modification on the second best site
    - `score_shifted_all_positions`: the score computed based on all possible shifted fragments (useful for identifying PSMs labeled with probes that can bind to multiple sites on the peptide, such as in some PAL data)
    - `position_scores`: a string with peptide sequence and scores when putting the modification on the specific site. For example `P(2.32)E(2.41)P(2.57)T(5.36)I(5.36)D(3.87)E(2.56)K(1.34)`.
    - `ions_all_unshifted`: the number of matched fragments when matching only unshifted (unmodified) fragments
    - `ions_best_position`: the number of matched fragments when putting the modification on the best site
    - `ions_second_best_position`: the number of matched fragments when putting the modification on the second best site
    - `ions_shifted_all_positions`: the number of matched fragments when putting the modification on all sites and matching all possible shifted (modification-containing) fragments
    - `score_shifted_best_position`: the score when putting the modification on the best site and matching only the shifted fragments
    - `ions_shifted_best_position`: the number of fragments when putting the modification on the best site and matching only the shifted fragments
    - `shifted_only_position_scores`: similar to `position_scores` but only matching shifted fragments
    - `shifted_only_position_ions`: similar to `shifted_only_position_scores` but showing the number of matched shifted fragments
- Add `analyzer_types` parameter
- Add a new mass calibration and parameter optimization mode, 4, for calibrating the mass and adjusting only the fragment mass tolerance
- Propagate instrument info to calibrated and uncalibrated mzML files
- Various bug fixes and improvements

## 4.0 - 2023-12-19
- Implement new MSFragger-DDA+ mode, triggered when DDA data is annotated as `DDA+` (MSFragger parameter `data_type=3`). MSFragger will perform full isolation window search, identifying multiple co-fragmented peptides from chimeric DDA spectra. This mode significantly boosts the number of IDs compared to conventional DDA search.
- Implement detailed mass-offset search mode. Each specified mass offset can have their own modification sites, neutral losses, and diagnostic ions.
- Overhaul the mass calibration and parameter optimization procedure for DIA data
- Significantly improve the ddaPASEF .d loading speed
- In the pin file, write all proteins in one column
- Extract and print isolation window sizes when checking the LC-MS files
- Replace ‘peptide_length’ score with Boolean peptide length scores (length `< 8`, `8`, `[9, 30]`, and `> 30`) in pin files
- Remove `log10_kl_negative_1` and `log10_kl_negative_2` from the DDA pin file
- Remove `add_topN_complementary` option
- Various bug fixes and improvements

## 3.8 - 2023-05-31
- Make the decoy prefix support `#`
- Add group FDR variable support
- Add `require_precursor` option for DIA data
- Add `reuse_dia_fragment_peaks` option for DIA data
- Remove the `output_report_topN` constraint for the DIA data
- For DIA data, do not remove precursor peaks when the isolation window larger than 20 Th
- Set `override_charge` to 0 for the first search
- Do not automatically set `remove_precursor_peak` to 0 for DIA data
- Various bug fixes and improvements

## 3.7 - 2023-01-12
- Add `write_uncalibrated_mgf` parameter that only works with .raw and .d formats
- Fix a bug reporting the incorrect `prevAA` and `nextAA` due to the clipped Methionine
- Various minor bug fixes and improvements

## 3.6 - 2022-12-03
- Require Java 9+
- Generate `_(un)calibrated.mzML` files. Stop generating `_(un)calibrated.mgf` files
- Various minor bug fixes and improvements

## 3.5 - 2022-05-27
- Require Java 9+
- Add `remainder_fragment_masses`, `activation_types`, and `min_sequence_matches` parameters
- Do not distinguish `I` and `L`
- Write ion mobility and compensation voltage to `<run name>.tsv` file.
- Add modification score to the pin file from open and mass-offset searches
- In pepXML file, change `native_id` to `SpectrumNativeId` to follow the pepXML schema
- For Thermo raw/mzML/mzXML data, using the native scan number as the scan number
- Clean up the protein description according to ProteinProphet's rule
- Print all decimal points in the pepxml files
- Various minor bug fixes and improvements

## 3.4 - 2021-10-30
- Support N-terminal enzymes
- Support two enzymes
- Adjust scores in pin files
- Automatically adjust `use_topN_peaks`, `minimum_ratio`, `output_report_topN`, `remove_precursor_peak`, `intensity_transform` and precursor tolerances for DIA mode
- Check data type by isolation windows width
- Add 450 and 500 top-N peaks to the parameter optimization for low-resolution data
- Optimize `max_fragment_charge` for low-resolution data
- Always write mass offsets to pepXML header for mass offset searches (to enable IonQuant after PTM-S)
- Various minor bug fixes and improvements

## 3.3 - 2021-07-22
- Support prmPASEF in Windows platform.
- Add `use_all_mods_in_first_search` parameter to use all specified variable modifications in first search.
- If users specify variable modifications on cysteine, use them in first search.
- Add `retentiontime`, `isotope_error`, and `mass_diff_score` columns to pin files.
- Remove `abs_mass_diff`, `matched_ion_fraction`, `delta_hyperscore`, and `abs_ppm` columns from pin files.
- Add `protein_descr` and `modified_peptide` attributes to pepXML file.
- Always write `calibrated.mgf` file for .raw and .d files.
- Do not write tsv file by default.
- Improve peak denoising for low-resolution MS2.
- Calibrating mass by median shift if there are only more than 100 high quality PSMs.
- Improve the parameter optimization step.
- Various minor bug fixes and improvements.

## 3.2 - 2021-03-09
- Add FAIMS support.
- Tracing fragment and refinement of scores in the DIA mode.
- Support directly searching DIA data without any MS1 scans in the DIA mode.
- Support fragment mass calibration in the DIA mode.
- Add `data_type = 0/1/2` option to specify data types: 0 = DDA (default), 1 = DIA, 2 = DIA with narrow windows (e.g. GPF data).
- Support removal of neutral loss fragment peaks (default), and add `deneutralloss = 0/1` option.
- Check MS2 resolution before the search.
- Require at least two sequence ions matched in the Glyco mode.
- Add `check_spectral_files = 0/1` option to turn on and off file checking.
- Always write `_calibrated/_uncalibrated.mgf` for ddaPASEF data (.d).
- Filter out scans outside of `[200, 15000]` range.
- Update pepXML schema to version 1.2.2.
- Improve help doc and change `--config` to `--config closed/open/nonspecific/glyco`.
- Remove `output_file_extension` option.
- Various minor bug fixes and improvements.

## 3.1.1 - 2020-10-01
- Fix a bug that does not write calibrated MGF.
- Fix a bug that do not allow labile modifications in mass offset search with `restrict_deltamass_to = all`.

## 3.1 - 2020-09-30
- New DIA search mode of MSFragger, supporting searching DIA data with parameter `precursor_mass_units = 2/3`.
- Precursor isotope error correction with parameter `precursor_mass_mode = corrected`.
- Support restricting delta mass (open/mass offset searches) to certain amino acids with parameter `restrict_deltamass_to`.
- Support putting localized delta mass to peptides as variable modifications with parameter `mass_diff_to_variable_mod = 0/1/2`. For N-Glyco data, will also put unlocalized glycans to the "N" of the first "N-X-S/T" sequon.
- Support pin format output, which is compatible with Percolator.
- Upgrade timsdata library (for Bruker timsTOF data) to 2.7.0.
- Write localization information to pepXML file with tag `ptm_result`.
- Added b~ and y~ fragment ions to localization (Glyco mode) 
- Reduce the PSMs required for mass calibration from 500 to 250, and increase the expectation threshold from 0.001 to 0.005.
- Improve parameter optimization procedure.
- Add a MS2 resolution check.
- Change "O"'s mass to pyrrolysine's mass, and print two comments for "O" and "U".
- Change the default value of `allowed_missed_cleavage` to 2.
- Change the default enzyme to stricttrypsin.
- Print more significant digits for masses and other key parameters in the output file.
- Various minor bug fixes and improvements.

## 3.0 - 2020-06-05
- New Glyco/Labile mode of MSFragger (for N-linked and O-linked glycopeptides; can also be used for other labile modifications).
- Change the default value of `write_calibrated_mgf` to 0.
- Add 7 ppm to nonspecific search's fragment tolerance list (optimization step).
- Various minor bug fixes and improvements.

## 2.4 - 2020-03-21
- Write original spectral file extension to pepXML after mass calibration.
- Write `native_id` to pepXML give mzML or mzXML file.
- Add 5 ppm and 50 ppm to the fragment mass tolerance list.
- Improve printed message.
- Support non-zero mass offsets in first search, mass calibration, and parameter optimization.
- Various minor bug fixes and improvements.

## 2.3 - 2020-01-30
- Add a MS/MS deisotoping module, with a new input file parameter `deisotope`. Default is set to 1 (use deisotoping).  
- Support water-loss ions: ion types `b-18` and `y-18`.
- Add one more column to variable modification setting specifying the maximum allowed number of instances of that particular  modification on the peptide.
- Replace `max_variable_mods_per_mod` with `max_variable_mods_per_peptide` that specifies the maximum allowed number of variable  
modifications on the peptide.  
- Print the number of peptide candidates with the number of modifications exceeding `max_variable_mods_combinations`.
- Print all decimal points to the tsv file.
- Change the minimum allowed `precursor_mass_lower` to -230 (in open search).
- Improvements in the parameter optimization procedure.
- Increase estimated memory usage by including the sizes of spectra and result.
- Various minor bug fixes and improvements.

## 2.2 - 2019-11-08
- Check spectral files at the beginning.
- Add a parameter (`write_calibrated_mgf`) to write calibrated spectra to MGF files.
- Add `uncalibrated_precursor_neutral_mass` attribute to pepXML file.
- Change the default value of `allow_multiple_variable_mods_on_residue` to `0`.
- Change the default values of `min_fragments_modelling` in open search to `2`.
- Change the default values of `min_matched_fragments` in open search to `4`.
- Limit the minimum value of `precursor_mass_lower` to -150 Da.
- Check `intensity_transform` and `remove_precursor_range` in parameter optimization step.
- Improve parameter optimization algorithm.
- Various minor bug fixes and improvements.

## 2.1 - 2019-09-08
- Fixed bugs.
- In parameter optimization step, improve the top-N peak candidates.

## 2.0 - 2019-09-05
- Switching from 'date' to 'version number' in naming released versions. This version is named 2.0 in recognition of the many improvements implemented in MSFragger in the last six months. 
- Support direct reading from Bruker raw files (.d folder).
- Support MGF file converted by Bruker DataAnalysis.
- FragPipe now supports running MSFragger with raw Thermo or Bruker files as input within FragPipe (limited functionality). 
- Pass ion mobility information (if applicable) from the spectral file (mzML, MGF, and .d folder) to the resulting pepXML file.
- New option to remove unfragmented precursor peaks from tandem mass spectra (`remove_precursor_peak` and `remove_precursor_range` parameters). Recommended option for ETD/EThcD data.
- New option to apply sqrt root transform to fragment ion intensities (`intensity_transform` parameter). Recommended option for ETD/EThcD data.
- Support calibrating precursor masses even when there are no MS1 scans in the input spectral file.
- Support assigning mass offsets to the localized amino acid sites.
- Add a `--version` flag to print version to console.
- Add a `--help` flag to print help information to console.
- Add a `--config` flag to write three fragger.params templates to current folder.
- Limit maximum precursor charge to 7.
- Various minor bug fixes and improvements.

## 20190628 - 2019-06-28
- Support direct reading from Thermo RAW files through the command line and the ProteomeDiscoverer node. FragPipe will be able to read raw files soon.
- Add an `excluded_scan_list_file` parameter that takes the path of a text file containing scan names. MSFragger would skip those scans if the path is not empty. Comment or delete this parameter name and its value if you do not want to use it.
- If there is no spectral file specified, generating pepindex and exiting.

## 20190530 - 2019-05-30
- Support mass calibration.
- Support optimal parameters finding.
- Support additional ion series including a-, b-, c-, x-, y-, and z-ions.
- Write localized modifications to `.tsv` file if `localize_delta_mass = 1`.
- Improve `.tsv` file's columns.
- Support command line parameters.
- Print parameters to the command line.
- Write parameters to the pepXML file.
- Re-implement alternative protein mapping for efficiency.
- Make the MGF file parsing more robust.
- Fix a bug about the inaccuracy of the searching speed printed to the command line.
- Showing the numbers of unique peptides in the command line.
- Various bug fixes and improvement.

## 20190222 - 2019-02-22
- Improved error messages for `OutOfMemoryError` and when too many peptides were generated durning digestion
- `report_alternative_proteins` option added. Turned off by default.
- write input file type in `msms_pipeline_analysis` tag, previously was hardcoded as `".mzXML"`
- write alternative proteins
- If MsAdjuster is used, output precursor intensity in `spectrum_query` tag
- added option to write both `TSV` and `pepXML` files.
   `output_format = tsv_pepXML`
- added `precursor_mass_mode` option

    usage:
    `precursor_mass_mode = isolated / selected / recalculated`
- default `shifted_ions_exclude_ranges` to `(-1.5, 3.5)`

## 20181110 - 2018-11-10
- update MSFTBX dependency

## 20180924 - 2018-09-24
- added `shifted_ions_exclude_ranges` option

  example usage:
  `shifted_ions_exclude_ranges = (-1.1033548378, -0.9033548378), (-0.1, 0.1), (0.9033548378, 1.1033548378), (1.9067096756, 2.1067096756), (2.9100645134, 3.1100645134), (15.894915, 16.094915), (42.905814, 43.105814)`
- added `output_location` option

## 20180924 - 2018-09-24
- `\n` is used as a newline for all platforms
- when in split search mode, output files in the working directory instead of the directory of input files

## 20180912 - 2018-09-12
- fragment matching is based on neutral masses, memory usage reduced
- restrictions on digested peptide size relaxed
- read in Corrector input if present
- directory for temporary files can be specified with `temp_location`
- non zero exit codes when terminating with error

## 20180316 - 2018-03-16
- Fix display issue with static terminal modifications.
- Open search times are reduced by about a quarter.
- Fixed bug with peptide mass calculation less termini.

## 20180224-RC1 - 2018-02-25
- MSFTBX upgraded to version 1.8.2.

## 20180223-RC1 - 2018-02-23 (public release)
- Java 9 compatible JAR
- Protein names are escaped to produce valid pepXML

## 20180215 - 2018-02-15
- Added support for mass offsets (enabling multi-notch searches)
