# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](http://keepachangelog.com/en/1.0.0/)

## 20190218 - 2019-02-18
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

## v20180224-RC1 - 2018-02-25
- MSFTBX upgraded to version 1.8.2.

## v20180223-RC1 - 2018-02-23 (public release)
- Java 9 compatible JAR
- Protein names are escaped to produce valid pepXML

## 20180215 - 2018-02-15
- Added support for mass offsets (enabling multi-notch searches)
