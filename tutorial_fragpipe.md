## Using FragPipe

##### FragPipe can be downloaded [here](https://github.com/Nesvilab/FragPipe/releases). Follow the instructions on that same Releases page to launch the program.

Before you get started, make sure your LC-MS file format is compatible with the workflows you want to perform (for Thermo data, we recommend [converting .raw files to mzML](https://msfragger.nesvilab.org/tutorial_convert.html)):

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/workflow_support.png)

#### Configure FragPipe
When FragPipe launches, the first tab in the window ('Config') will be used to configure the program.
1. Connect FragPipe to a MSFragger .jar program file. If you already have such a file downloaded, use the 'Browse' button to select it or 'Update' to upgrade to the latest version. If you have not downloaded MSFragger before, use the 'Download' button. [(MSFragger installation help)](http://msfragger.nesvilab.org/tutorial_setup_fragpipe.html#install-update-or-use-an-already-downloaded-version-of-msfragger)
2. Connect FragPipe to a Philosopher program file. If you already have it downloaded, select 'Browse', otherwise select 'Download'. [(Philosopher installation help)](http://msfragger.nesvilab.org/tutorial_setup_fragpipe.html#install-update-or-use-an-already-downloaded-version-of-philosopher)
3. Optional: Python is needed to perform database splitting (necessary in complex searches/low memory situations) and spectral library generation. If you already have Python 3 or greater plus a few additional packages installed (**numpy**, **pandas**, **Cython**, and **msproteomicstools**) use 'Browse' to locate your python.exe file. [(Python installation help)](https://msfragger.nesvilab.org/tutorial_setup_fragpipe.html#optional-install-update-or-use-an-already-installed-version-of-python) 

For more help, see the full [tutorial on FragPipe configuration](https://msfragger.nesvilab.org/tutorial_setup_fragpipe.html).

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/fragpipe_tutorial-config.png)
 

 <br>

#### Select workflow & add spectral files
In the 'Workflow' tab:
1. Choose the workflow you want to use and press 'Load'. A number of common workflows (including [glyco](https://msfragger.nesvilab.org/tutorial_glyco-fragger.html)) are provided, or you can customize, save and load workflows for future use (via the 'workflows' folder).
2. Set the amount of memory & number of logical cores to use.
3. Set 'Regular MS' for non-ion mobility data, and 'IM-MS' for Bruker timsTOF PASEF data.
4. Drag & drop LC/MS files into the window or select 'Add files' or 'Add Folder Recursively' (to add all files in a folder, including those in subfolders).  Specify the appropriate labels for the replicates/fractions in your experiment.

**Notes about timsTOF data:** For raw PASEF files (.d extension), each data file is a folder, so you may find ‘Add Folder Recursively’ useful. If you have already run MSFragger on the .d files, make sure the .mzBIN files resulting from that analysis are in the same directory as the .d files to speed up the analysis (make sure to remove any .d folders from the input list before continuing). If you don't need to perform quantification, .mgf or _calibrated.mgf_ files can be used instead of raw .d.

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/fragpipe_tutorial-workflow.png)

<br>
 
Once you've loaded your spectral files, indicate how you'd like PSM/peptide/protein reports to be generated:

##### For a single set of reports (search results from all input files merged)
Leave the 'Experiment' and 'Replicate' fields blank, and ensure that the 'Multi-Experiment Report' box on the 'Report' tab is not checked.

##### For reports with results from different fractionated replicates shown in separate columns
Indicate the 'Experiment' and 'Replicate' for each input file as shown below, where each replicate of two experimental conditions is composed of two fractions. Different fractions from the same sample should have the same 'Experiment'/'Replicate' name. On the 'Report' tab, check 'Multi-Experiment Report'.

| Path            | Experiment | Replicate |
|-----------------|------------|-----------|
| run_name_1.mzML | Control    | 1         |
| run_name_2.mzML | Control    | 1         |
| run_name_3.mzML | Control    | 2         |
| run_name_4.mzML | Control    | 2         |
| run_name_5.mzML | Treatment  | 3         |
| run_name_6.mzML | Treatment  | 3         |
| run_name_7.mzML | Treatment  | 4         |
| run_name_8.mzML | Treatment  | 4         |

**Note:** the 'Replicate' ID (e.g., 1, 2, 3, and 4 in the above table) should not be reused by different replicates from different experiments. However, if each pair of 'Control' and 'Treatment' is from the same study subject, you should use the same 'Replicate' ID for the corresponding 'Control' runs and 'Treatment' runs (detailed discussion can be found from [https://github.com/Nesvilab/FragPipe/issues/183](https://github.com/Nesvilab/FragPipe/issues/183). We appreciate @tobiasko for the suggestion.):

| Path            | Experiment | Replicate |
|-----------------|------------|-----------|
| run_name_1.mzML | Control    | 1         |
| run_name_2.mzML | Control    | 1         |
| run_name_3.mzML | Control    | 2         |
| run_name_4.mzML | Control    | 2         |
| run_name_5.mzML | Treatment  | 1         |
| run_name_6.mzML | Treatment  | 1         |
| run_name_7.mzML | Treatment  | 2         |
| run_name_8.mzML | Treatment  | 2         |

where 'run_name_1.mzML', 'run_name_2.mzML', 'run_name_5.mzML', and 'run_name_6.mzML' are controls and treatments from the same study subject; 'run_name_3.mzML', 'run_name_4.mzML', 'run_name_7.mzML', and 'run_name_8.mzML' are controls and treatments from another study subject. 
<br>

**Note:** for compatibility with the Resource for Evaluation of Protein Interaction Networks ([REPRINT](https://reprint-apms.org/)), 'Experiment' names should be written as follows:

Negative controls: `CONTROL_1`, `CONTROL_2`, `CONTROL_3`, etc.

Bait IPs: `[GENE]_[replicate]`, where `[GENE]` is the official gene symbol of the protein, e.g. `HDAC5_1`. If there are multiple conditions for the same bait protein (e.g. mutant and wt), use `HDAC5_wt_1` and `HDAC5_mutant_1` format.
 <br>

 
#### Specify a protein sequence database
If you haven't made a database file using FragPipe/Philosopher before, select 'Download' to fetch one from Uniprot. Specify the download location, then choose your options and select an organism (use the uniprot proteome ID to specify your own, e.g. 'UP000000625' for E. coli).

Use 'Browse' to select a FASTA file from a previous FragPipe/Philosopher analysis.

If you need to use a custom FASTA database, it must follow a certain format and contain decoy sequences. Click 'Browse' to navigate to your custom FASTA. If you select 'Try Auto-Detect', 50% of the entries should contain the decoy tag. For help adding decoys and database formatting, see the instructions on the 'Database' tab or [here](https://github.com/Nesvilab/philosopher/wiki/Database).

  
![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/fragpipe_tutorial-database.png)


 <br>

#### Set MSFragger search parameters
In the 'MSFragger' tab, check that the search parameters are suitable for your analysis. You can choose to save a customized parameter file to load for future use, or save the entire workflow (from either the 'Workflow' or the 'Run' tab).
   
**Note:** For non-specific searches or for searches with many variable modifications, you may need to use the database splitting option, which requires an installation of [Python](https://msfragger.nesvilab.org/tutorial_setup_fragpipe.html#optional-install-update-or-use-an-already-installed-version-of-python).

 
![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/fragpipe_tutorial-msfragger.png)
 
 
 <br>

#### Validation
If you previously updated the downstream parameters when setting MSFragger search parameters, you can skip to the next section. You can also load default downstream processing parameters by selecting the appropriate 'Load defaults' button. In most cases, search results from MSFragger must be filtered by [PeptideProphet](http://peptideprophet.sourceforge.net/) and [ProteinProphet](http://proteinprophet.sourceforge.net/).

For open search workflows, select [Crystal-C](https://www.nesvilab.org/Crystal-C/) to remove open search artifacts and improve the interpretability of your results.

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/fragpipe_tutorial-validation.png)


 <br>
 
#### Quantification
To perform quantification, make sure Label-Free Quantification and/or Isobaric Labeling-Based Quantification are selected in their respective tabs (note that workflows can be performed without any quantification, in which case spectral counts will be reported).

For **label-free quantification**, a match-between-runs (MBR) option through [IonQuant](http://ionquant.nesvilab.org/) can be turned on.

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/fragpipe_tutorial-lfq.png)

For **label-based quantification**, 
1. Select a labeling reagent.
2. For each experiment as set in the 'Workflow' tab, select 'Edit/Create' Sample/Channel Annotation to assign sample information to each TMT/iTRAQ channel.

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/fragpipe_tutorial-labelquant.png)

In the annotation pop-up window:
1. Load the selected TMT/iTRAQ channels.
2. Provide the experiment/replicate information for each channel.

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/fragpipe_tutorial-labelquant-annotate.png)


 <br>

#### PTMs
For open search-based workflows, [PTM-Shepherd](https://github.com/Nesvilab/PTM-Shepherd/wiki/PTM-Shepherd) summarizes delta masses and provides reports on residue localization, retention time similarity, and more.

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/fragpipe_tutorial-ptmshepherd.png)

 <br>

#### Spectral library generation
Spectral libraries can be generated within closed search-based workflows.

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/fragpipe_tutorial-speclib.png)

 <br>

#### Run FragPipe
1. Browse for the folder where you would like the search results to be written.
2. Press 'RUN' to begin the analysis! See the MSFragger [wiki](https://github.com/Nesvilab/MSFragger/wiki), [FAQ](https://github.com/Nesvilab/MSFragger/wiki/Frequently-Asked-Questions), and previous questions on [Github](https://github.com/Nesvilab/FragPipe/issues?utf8=%E2%9C%93&q=) for more help.


![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/fragpipe_tutorial-run.png)
 

