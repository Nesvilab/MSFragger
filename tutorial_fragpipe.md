## Using FragPipe

##### FragPipe can be downloaded [here](https://github.com/Nesvilab/FragPipe/releases). Follow the instructions on that same Releases page to launch the program.

Before you get started, make sure your LC-MS file format is compatible with the workflows you want to perform (for Thermo data, we recommend [converting .raw files to mzML](https://msfragger.nesvilab.org/tutorial_convert.html)):

<img src="https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/workflow_support.png" width="450px" align="middle"/>
<br>

#### Tutorial contents
* [Configure FragPipe](https://msfragger.nesvilab.org/tutorial_fragpipe.html#configure-fragpipe)
* [Select workflow and add spectral files](https://msfragger.nesvilab.org/tutorial_fragpipe.html#select-workflow-and-add-spectral-files)
  * [Single-experiment report](https://msfragger.nesvilab.org/tutorial_fragpipe.html#single-experiment-report)
  * [Multi-experiment report](https://msfragger.nesvilab.org/tutorial_fragpipe.html#multi-experiment-report)
  * [Affinity purification data](https://msfragger.nesvilab.org/tutorial_fragpipe.html#affinity-purification-data)
  * [TMT/iTRAQ data](https://msfragger.nesvilab.org/tutorial_fragpipe.html#tmtitraq-data)
* [Specify a sequence database](https://msfragger.nesvilab.org/tutorial_fragpipe.html#specify-a-protein-sequence-database)
* [Configure MSFragger search](https://msfragger.nesvilab.org/tutorial_fragpipe.html#configure-msfragger-search)
* [Validation](https://msfragger.nesvilab.org/tutorial_fragpipe.html#validation)
* [Label-free quantification](https://msfragger.nesvilab.org/tutorial_fragpipe.html#lfq-label-free-quantification)
* [Isobaric quantification](https://msfragger.nesvilab.org/tutorial_fragpipe.html#isobaric-labeling-based-quantification)
* [Post-translational modifications](https://msfragger.nesvilab.org/tutorial_fragpipe.html#ptms)
* [Spectral library generation](https://msfragger.nesvilab.org/tutorial_fragpipe.html#spectral-library-generation)
* [Run FragPipe](https://msfragger.nesvilab.org/tutorial_fragpipe.html#run-fragpipe)
<br>

### Configure FragPipe
When FragPipe launches, the first tab in the window ('Config') will be used to configure the program.
1. Connect FragPipe to a MSFragger .jar program file. If you already have such a file downloaded, use the 'Browse' button to select it or 'Update' to upgrade to the latest version. If you have not downloaded MSFragger before, use the 'Download' button. [(MSFragger installation help)](http://msfragger.nesvilab.org/tutorial_setup_fragpipe.html#install-update-or-use-an-already-downloaded-version-of-msfragger)
2. Connect FragPipe to a Philosopher program file. If you already have it downloaded, select 'Browse', otherwise select 'Download'. [(Philosopher installation help)](http://msfragger.nesvilab.org/tutorial_setup_fragpipe.html#install-update-or-use-an-already-downloaded-version-of-philosopher)
3. Optional: Python is needed to perform database splitting (necessary in complex searches/low memory situations) and spectral library generation. If you already have Python 3 or greater plus a few additional packages installed (**numpy**, **pandas**, **Cython**, and **msproteomicstools**) use 'Browse' to locate your python.exe file. [(Python installation help)](https://msfragger.nesvilab.org/tutorial_setup_fragpipe.html#optional-install-update-or-use-an-already-installed-version-of-python) 

For more help, see the full [tutorial on FragPipe configuration](https://msfragger.nesvilab.org/tutorial_setup_fragpipe.html).

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/fragpipe_tutorial-config.png)
 

 <br>

### Select workflow and add spectral files

In the 'Workflow' tab:

1. Choose the workflow you want to use and press 'Load'. Use **Default** workflow for simple conventional (closed) searches. A number of common workflows (including [glyco](https://msfragger.nesvilab.org/tutorial_glyco-fragger.html)) are provided. You can also customize and save workflows for future use (all workflows are stored in the FragPipe 'workflows' folder). You can even share your workflow files with other FragPipe users. 

2. Set the amount of memory & number of logical cores to use.

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/fragpipe_tutorial-workflow.png)


3. Set 'Regular MS' for non-ion mobility data, and 'IM-MS' for Bruker timsTOF PASEF data.

4. Drag & drop LC/MS files into the window or select 'Add files' or 'Add Folder Recursively' (to add all files in a folder, including those in subfolders).  Specify the appropriate labels for the replicates/fractions in your experiment.

**Notes about timsTOF data:** With timsTOF PASEF data we recommend using raw PASEF files (.d files). You can simply select .d folder as the raw file. If you have already run MSFragger on the .d files, make sure the .mzBIN files resulting from that analysis are in the same directory as the .d files to speed up the analysis. If you don't need to perform quantification, you can use .mgf files (that can optionally be generated by the Bruker's software immediately after data acquisition is completed) instead of raw .d.
 
Once you've loaded your spectral files, annotate your data to specify Experiments and Replicates, which determines how your PSM/peptide/protein etc. reports will be generated:

#### Single-experiment report 
Leave the 'Experiment' and 'Replicate' fields blank. Use this option if you want to analyze all input files together and generate a single merged report (including bulding a combined spectral library from all input data). 

#### Multi-experiment report
Indicate the 'Experiment' and 'Replicate' for each input file as shown below, where each replicate of two experimental conditions is composed of two fractions. Different fractions from the same sample should have the same 'Experiment'/'Replicate' name.

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

**Note:** If you would like to use MSStats for downstream statistical analysis of FragPipe-generated reports, the 'Replicate' ID (e.g., 1, 2, 3, and 4 in the above table) should not be reused by different replicates from different experiments. However, if each pair of 'Control' and 'Treatment' is from the same study subject, you should use the same 'Replicate' ID for the corresponding 'Control' runs and 'Treatment' runs (detailed discussion can be found [here](https://github.com/Nesvilab/FragPipe/issues/183).):

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
<br>

#### Affinity-purification data
When analyzing AP-MS and related data (e.g. BioID) for compatibility with the Resource for Evaluation of Protein Interaction Networks ([REPRINT](https://reprint-apms.org/)), 'Experiment' names should be written as follows:

Negative controls: Put Control (or CONTROL) in the Experiment column, and label each biological replicate with a different replicate number.

Bait IPs: Use `[GENE]_[condition]` format to describe the experiments, where `[GENE]` is the official gene symbol of the bait protein, e.g. `HDAC5`. If there are multiple conditions for the same bait protein (e.g. mutant and wt), add can add 'condition', e.g. `HDAC5_mut`.

| Path            | Experiment | Replicate |
|-----------------|------------|-----------|
| run_name_1.mzML | Control    | 1         |
| run_name_2.mzML | Control    | 2         |
| run_name_3.mzML | Control    | 3         |
| run_name_4.mzML | HDAC5      | 1         |
| run_name_5.mzML | HDAC5      | 2         |
| run_name_6.mzML | HDAC5      | 3         |
| run_name_7.mzML | HDAC5_mut  | 1         |
| run_name_8.mzML | HDAC5_mut  | 2         |
| run_name_9.mzML | HDAC5_mut  | 3         |

<br>

Note that all negative controls should be labeled the same, as 'Control', even if you have negative controls generated under different conditions or in different cell lines.  

 <br>


#### TMT/iTRAQ data
For TMT/iTRAQ analysis, spectral files should be in mzML format. Raw format is currently not supported.

TMT/iTRAQ experiments typically consist of one or more 'plexes' (multiplexed samples), each composed of multiple spectral files (from prefractionation). Use'Experiment' to denote spectral files from the same plex while leaving the 'Replicate' column empty. We recommend organizing data in folders, one for each plex. E.g. if you have 2 TMT plexes, with 2 spectral files (peptide fractions) in each, you can create a folder (e.g. named 'MyData'), containing two subfolders (e.g. 'TMT1' and 'TMT2') each containing the corresponding mzML files. Load data by clicking **Add folder recursively** and selecting 'MyData' folder, then assign files to Experiments/Groups **By parent directory**, resulting in the following spectral file annotation:   

| Path                 | Experiment | Replicate |
|----------------------|------------|-----------|
| run_name_tmt1_1.mzML | TMT1       |           |
| run_name_tmt1_2.mzML | TMT1       |           |
| run_name_tmt2_1.mzML | TMT2       |           |
| run_name_tmt2_2.mzML | TMT2       |           |

 <br>
 
### Specify a protein sequence database
If you haven't made a database file using FragPipe/Philosopher before, select 'Download' to fetch one from UniProt. Specify the download location, then choose your options and select an organism (use the uniprot proteome ID to specify your own, e.g. 'UP000000625' for E. coli). We generally recommend using 'Reviewed' subset of UniProt. If needed, add iRT sequences (e.g. if you are building a spectral library for DIA analysis and added iRT peptides to your samples).   

You can use 'Browse' to select a FASTA file from a previous FragPipe/Philosopher analysis.

If you need to use a custom FASTA database, it must follow a certain format and contain decoy sequences. Click 'Browse' to navigate to your custom FASTA. If you select 'Try Auto-Detect', 50% of the entries should contain the decoy tag. For help adding decoys and database formatting, see the instructions on the 'Database' tab or [here](https://github.com/Nesvilab/philosopher/wiki/Database).

  
![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/fragpipe_tutorial-database.png)


 <br>

### Configure MSFragger search
In the 'MSFragger' tab, check that the search parameters are suitable for your analysis. You can choose to save a customized parameter file to load for future use, or save the entire workflow (from either the 'Workflow' or the 'Run' tab).
   
**Note:** For non-specific searches or for searches with many variable modifications, you may need to use the database splitting option, which requires an installation of [Python](https://msfragger.nesvilab.org/tutorial_setup_fragpipe.html#optional-install-update-or-use-an-already-installed-version-of-python).

 
![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/fragpipe_tutorial-msfragger.png)
 
 
 <br>

### Validation
If you loaded one of the common workflow file provided with FragPipe, or previously updated the downstream parameters when setting MSFragger search parameters, you can skip to the next section. You can also load default downstream processing parameters by selecting the appropriate 'Load defaults' button. In most cases, search results from MSFragger must be filtered by [PeptideProphet](http://peptideprophet.sourceforge.net/) and [ProteinProphet](http://proteinprophet.sourceforge.net/).

For open search workflows, select [Crystal-C](https://www.nesvilab.org/Crystal-C/) to remove open search artifacts and improve the interpretability of your results (Note: at present, Crystal-C does not support .d files, and will be disabled by FragPipe when using .d as input).

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/fragpipe_tutorial-validation.png)


 <br>
 
### LFQ: Label-free Quantification

To perform label-free quantification, make sure Label-Free Quantification is selected (note that analyses can be performed without any quantification, in which case spectral counts will be reported). 

[IonQuant](http://ionquant.nesvilab.org/) is a default LFQ quantification tool in FragPipe. A match-between-runs (**MBR**) option can be turned on for closed search workflows. **Min ions** (default = 2) controls how many quantifiable ions are required for protein-level quantification. Select **Protein quant** quantification option (either top-N, e.g. summation of the top 3 most intense peptides, or MaxLFQ approach. The latter is recommended). 

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/fragpipe_tutorial-lfq.png)

### Isobaric Labeling-Based Quantification 

To perform isobaric labeling-based quantification (TMT/iTRAQ), make sure Label-Free Quantification is selected
1. Select a labeling reagent (e.g. TMT10, TMT6, iTRAQ4, etc).
2. For each experiment as set in the 'Workflow' tab, select 'Edit/Create' Sample/Channel Annotation to assign sample information to each TMT/iTRAQ channel, or 'Browse' to load an existing 'annotation.txt' file.

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/fragpipe_tutorial-labelquant.png)

In the annotation pop-up window:
1. Load the selected TMT/iTRAQ channels.
2. Provide the experiment/replicate information for each channel.
![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/fragpipe_tutorial-labelquant-annotate.png)

Annotation files will be named 'annotation.txt' and saved in each folder.

**Note:** Instead of naming samples/channels in FragPipe using Edit/Create, you can make 'annotation.txt' files in advance, and FragPipe will load it automatically if it is in the same folder as the corresponding mzML files. 

If you have multiple plexes and want to use a common (Bridge) channel, select 'Define reference: Reference sample', and enter the text keyword describing the Bridge channel (e.g. 'pool') that matches your naming scheme. Alternatively, select 'Virtual' reference sample approach if you do not have a pooled channel.   


### PTMs
For open search-based workflows, [PTM-Shepherd](https://github.com/Nesvilab/PTM-Shepherd/wiki/PTM-Shepherd) summarizes delta masses and provides reports on residue localization, retention time similarity, and more.

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/fragpipe_tutorial-ptmshepherd.png)

 <br>

### Spectral library generation
Spectral libraries can be generated within closed search-based workflows. A library will be generated for each experiment specified in the 'Workflow' tab. Experiments must contain more than one spectral file.

When building a library from fractionated data, using one of the fractions for reference retention time (RT) calibration is not recommended. Instead, select ciRT for human samples or iRT spike-in peptides for other organisms if possible.

**Note:** To use EasyPQP, you will need to update to the latest version. Open an Anaconda Prompt command line window and run these two commands:

`pip uninstall --yes easypqp`

`pip install git+https://github.com/grosenberger/easypqp.git@master`


![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/fragpipe_tutorial-speclib.png)

 <br>

### Run FragPipe
1. Browse for the folder where you would like the search results to be written.
2. Press 'RUN' to begin the analysis! See the MSFragger [wiki](https://github.com/Nesvilab/MSFragger/wiki), [FAQ](https://github.com/Nesvilab/MSFragger/wiki/Frequently-Asked-Questions), and previous questions on [Github](https://github.com/Nesvilab/FragPipe/issues?utf8=%E2%9C%93&q=) for more help.


![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/fragpipe_tutorial-run.png)
 

