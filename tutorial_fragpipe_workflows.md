### FragPipe workflows

#### [FragPipe](https://fragpipe.nesvilab.org/) can be downloaded [here](https://github.com/Nesvilab/FragPipe/releases). Follow the instructions on that same Releases page to launch the program.

Below is an alphabetical list of the analysis workflows provided with FragPipe. Any of these workflows can be customized and saved for later use, each customized workflow should be saved with a unique name.


##### Basic search (Default)
Simple closed search, no quantification. MSFragger search with 'stricttrypsin' (Trypsin/P) enzyme, fully tryptic peptides only, up to 2 missed cleavages. Met oxidation and protein N-term Acetyl specified as variable modifications, and C+57 as fixed modification. Deisotoping, mass calibration, and parameter optimization are enabled. Post-processing with Philosopher (PeptideProphet, ProteinProphet), with 1% FDR filtering at the PSM and protein levels (sequential filtering).
<br>

##### DIA-MSFragger spectral library building (DIA-MSFragger_SpecLib)
MSFragger DIA mode. Recommended options for narrow-window DIA data (using 3 highest scoring hits for each MS/MS spectrum). FDR filtering to 1% at all levels (protein, peptide, PSM) using 2D, picked FDR filtering. Spectral library building with EasyPQP to generate a Spectronaut and DIA-NN compatible spectral library for subsequent quantification using those tools.
Default is RT alignment using commonly observed peptides (ciRT). Alternatively (recommended for non-human data), when building a library from narrow-window DIA runs, include one (or more) wide-window DIA runs, and choose "Automatic selection of a run as Reference' in EasyPQP. All runs will then be aligned to the reference wide-window DIA run.
<br>

##### DIA-Umpire spectral library building (DIA-Umpire_Speclib)
DIA-Umpire based workflow for direct DIA analysis. Requires mzXML files as input. Pseudo-MS/MS spectra are extracted with DIA-Umpire SE module, and searched using MSFragger. 1% FDR filtering at all levels (protein, peptide) using 2D, picked FDR strategy. EasyPQP for generating a spectral library compatible with Spectronaut and DIA-NN for subsequent quantification using those tools.
<br>

##### Basic search & quantification (LFQ)
Perform closed search, followed by label free quantification with IonQuant. Need to choose the right MS data type (Regular MS vs IM-MS).
<br>

##### Basic search & quantification with match-between-runs (LFQ-MBR)
Perform closed search, followed by label free quantification and match-between-runs with IonQuant. Need to choose the right MS data type (Regular MS vs IM-MS) and assign experiments to runs.
<br>

##### HLA peptide search (Nonspecific-HLA)
Nonspecific search, with recommended settings for HLA peptides. Peptide length 7-25. MSFragger search assumes cysteines were not alkylated (i.e. samples were not treated with iodoacetamide). Cysteinylation (C+119) is specified as variable modification. Protein FDR filter is not applied, so each output file (PSM, ion, peptide) is filtered to 1% FDR at that level. 
<br>

##### Peptidome search (Nonspecific-peptidome)
Nonspecific search, with recommended settings for peptidome data (plasma, CSF, etc.). Peptide length 7-65. MSFragger search assumes cysteines were alkylated. Met oxidation, C-term amidation, and Pyro-Glu are specified as variable modifications. Protein FDR filter is not applied, so each output file (PSM, ion, peptide) is filtered to 1% FDR at that level.
<br>

##### Basic open search (Open)
Open search workflow for PTM analysis. MSFragger localization-aware open search (LOS) algorithm, with deisotoping, mass calibration, parameter optimization, and monoisotope correction enabled. Mass range -150 to 500 Da, with Met oxidation and protein N-term Acetyl included as variable modifications. PeptideProphet with extended mass model. Crystal-C for artifact removal. PTM-Shepherd for mass shift summarization. 
<br>

##### TMT-10 quantification (TMT10)
Basic TMT 10-plex workflow, with identification and quantification from high mass accuracy MS2. Met oxidation, protein N-term Acetyl, n-term TMT, and TMT on S ("overlabeling") are specified as variable modifications. TMT-Integrator with virtual reference approach, median-centering normalization, data summarization at the gene level. If a reference/bridge sample is available, specify the corresponding channel/sample name tag in the annotation file(s) and in TMT-Integrator tab. 
<br>

##### TMT-10 MS3 quantification (TMT10-MS3)
TMT 10-plex workflow, with quantification from MS3 and identification from low mass accuracy MS2. Met oxidation, protein N-term Acetyl, and n-term TMT are specified as variable modifications. TMT-Integrator with virtual reference approach, median-centering normalization, data summarization at the gene level. If a reference/bridge sample is available, specify the corresponding channel/sample name tag in the annotation file(s) and in TMT-Integrator tab. 
<br>

##### Phospho TMT-10 MS3 quantification (TMT10-MS3-phospho)
TMT 10-plex workflow for phosphopeptide enriched data, with quantification from MS3 and identification from low resolution MS2. PTMProphet for site localization. TMT-Integrator with virtual reference approach, median-centering normalization, data summarization at the gene/protein/peptide/site levels. If a reference/bridge sample is available, specify the corresponding channel/sample name tag in the annotation file(s) and in TMT-Integrator tab.
<br>

##### TMT-10 quantification with bridge/pooled sample (TMT10-bridge)
TMT 10-plex, quantification and identification from high mass accuracy MS2. Met oxidation, protein N-term Acetyl, n-term TMT, and TMT on S ("overlabeling") are specified as variable modifications. TMT-Integrator with Bridge channel (labeled as 'pool' in the annotation files), data summarization at the gene level. Printing results with three normalization options (None; MD: Median Centering; GN: median centering with MAD variance scaling.
<br>

##### Phospho TMT-10 quantification (TMT10-phospho)
TMT 10-plex workflow for phosphopeptide enriched data, with quantification from MS2. PTMProphet for site localization. TMT-Integrator with virtual reference approach, median-centering normalization, data summarization at the gene/protein/peptide/site levels. If a reference/bridge sample is available, specify the corresponding channel/sample name tag in the annotation file(s) and in TMT-Integrator tab.
<br>

##### Phospho TMT-10 quantification with bridge/pooled sample (TMT10-phospho-bridge)
TMT 10-plex workflow for phosphopeptide enriched data, with quantification from MS2. PTMProphet for site localization. TMT-Integrator with Bridge channel (labeled as 'pool' in the annotation files), median-centering normalization, data summarization at the gene/protein/peptide/site levels. 
<br>

##### TMT-16 quantification (TMT16)
Basic TMT 16-plex workflow, with quantification and identification from MS2. Met oxidation, protein N-term Acetyl, n-term TMT are specified as variable modifications. TMT-Integrator with virtual reference approach, median-centering normalization, data summarization at the gene level. If a reference/bridge sample is available, specify the corresponding channel/sample name tag in the annotation file(s) and in TMT-Integrator tab. 
<br>

##### TMT-16 MS3 quantification (TMT16-MS3)
Basic TMT 16-plex workflow, with quantification from MS3 and identification form low mass accuracy MS2 (ion trap).
Met oxidation, protein N-term Acetyl, n-term TMT are specified as variable modifications. TMT-Integrator with virtual reference approach, median-centering normalization, data summarization at the gene level. If a reference/bridge sample is available, specify the corresponding channel/sample name tag in the annotation file(s) and in TMT-Integrator tab.
<br>

##### Mass shift search (common-mass-offsets)
Mass Offset (also known as Multinotch) search workflow for a fast search for most common modifications (list of mass shifts specified in MSFragger 'Mass Offset' field). MSFragger localization-aware open search (LOS) algorithm, filtered to report PSMs with specified mass shifts only (with isotope errors allowed). No variable modifications are specified. Mass calibration, parameter optimization, and precursor monoisotope error correction are enabled. PeptideProphet with extended mass model. PTM-Shepherd for mass shift summarization. 
<br>

##### N-glycopeptide search (glyco-N-HCD)
For CID/HCD search of enriched N-glycopeptides. Met oxidation and protein N-term Acetyl specified as variable modifications, and C+57 as fixed modification. Deisotoping, mass calibration, and parameter optimization are enabled. Post-processing with Philosopher (PeptideProphet with extended mass model, ProteinProphet), with 1% FDR filtering at the PSM and protein levels (sequential filtering). PTM-Shepherd used for summarization.
<br>

##### N-glycopeptide search, hybrid activation (glyco-N-Hybrid)
For hybrid activation (EThcD, etc) search of enriched N-glycopeptides. Met oxidation and protein N-term Acetyl specified as variable modifications, and C+57 as fixed modification. Deisotoping, mass calibration, and parameter optimization are enabled. Post-processing with Philosopher (PeptideProphet with extended mass model, ProteinProphet), with 1% FDR filtering at the PSM and protein levels (sequential filtering). PTM-Shepherd used for summarization.
<br>

##### N-glycopeptide open search (glyco-N-open-HCD)
For CID/HCD open search of enriched N-glycopeptides. Mass range -200 to +4,000 Da, Met oxidation and protein N-term Acetyl specified as variable modifications, and C+57 as fixed modification. Deisotoping, mass calibration, and parameter optimization are enabled. Post-processing with Philosopher (PeptideProphet with extended mass model, ProteinProphet), with 1% FDR filtering at the PSM and protein levels (sequential filtering). PTM-Shepherd used for summarization.
<br>

##### N-glycopeptide open search, hybrid activation (glyco-N-Hybrid)
For hybrid activation (EThcD, etc) open search of enriched N-glycopeptides. Mass range -200 to +4,000 Da, Met oxidation and protein N-term Acetyl specified as variable modifications, and C+57 as fixed modification. Deisotoping, mass calibration, and parameter optimization are enabled. Post-processing with Philosopher (PeptideProphet with extended mass model, ProteinProphet), with 1% FDR filtering at the PSM and protein levels (sequential filtering). PTM-Shepherd used for summarization.
<br>

##### N-glycopeptide search & quantification (glyco-N-quant-HCD)
For CID/HCD search and quantification of enriched N-glycopeptides. Met oxidation and protein N-term Acetyl specified as variable modifications, and C+57 as fixed modification. Deisotoping, mass calibration, and parameter optimization are enabled. Post-processing with Philosopher (PeptideProphet with extended mass model, ProteinProphet), with 1% FDR filtering at the PSM and protein levels (sequential filtering). Label-free quantification with IonQuant. PTM-Shepherd used for summarization.
<br>

##### O-glycopeptide search (glyco-O-HCD)
For CID/HCD search of enriched O-glycopeptides. Met oxidation and protein N-term Acetyl specified as variable modifications, and C+57 as fixed modification. Deisotoping, mass calibration, and parameter optimization are enabled. Post-processing with Philosopher (PeptideProphet with extended mass model, ProteinProphet), with 1% FDR filtering at the PSM and protein levels (sequential filtering). PTM-Shepherd used for summarization.
<br>

##### O-glycopeptide search, hybrid activation (glyco-O-Hybrid)
For hybrid activation (EThcD, etc) search of enriched O-glycopeptides. Met oxidation and protein N-term Acetyl specified as variable modifications, and C+57 as fixed modification. Deisotoping, mass calibration, and parameter optimization are enabled. Post-processing with Philosopher (PeptideProphet with extended mass model, ProteinProphet), with 1% FDR filtering at the PSM and protein levels (sequential filtering). PTM-Shepherd used for summarization.
<br>

##### O-glycopeptide open search (glyco-O-open-HCD)
For CID/HCD open search of enriched O-glycopeptides. Mass range -200 to +4,000 Da, Met oxidation and protein N-term Acetyl specified as variable modifications, and C+57 as fixed modification. Deisotoping, mass calibration, and parameter optimization are enabled. Post-processing with Philosopher (PeptideProphet with extended mass model, ProteinProphet), with 1% FDR filtering at the PSM and protein levels (sequential filtering). PTM-Shepherd used for summarization.
<br>

##### O-glycopeptide open search, hybrid activation (glyco-O-Hybrid)
For hybrid activation (EThcD, etc) open search of enriched O-glycopeptides. Mass range -200 to +4,000 Da, Met oxidation and protein N-term Acetyl specified as variable modifications, and C+57 as fixed modification. Deisotoping, mass calibration, and parameter optimization are enabled. Post-processing with Philosopher (PeptideProphet with extended mass model, ProteinProphet), with 1% FDR filtering at the PSM and protein levels (sequential filtering). PTM-Shepherd used for summarization.
<br>

##### iTRAQ search and quantification (iTRAQ4)
Closed search and basic iTRAQ 4-plex workflow, with quantification from MS2. TMT-Integrator with virtual reference approach, median-centering normalization, data summarization at the gene level. 
<br>
<br>

#### Next: see the [FragPipe usage tutorial](https://msfragger.nesvilab.org/tutorial_fragpipe.html).