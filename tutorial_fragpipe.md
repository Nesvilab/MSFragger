## Performing a database search with FragPipe

##### FragPipe can be downloaded [here](https://github.com/Nesvilab/FragPipe/releases). Follow the instructions on that same Releases page to launch the program.

Before you get started, make sure your LC-MS file format is compatible with the workflows you want to perform:

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/workflow_support.png)

#### Configure FragPipe:
When FragPipe launches, the first tab in the window ('Config') will be used to configure the program.
1. Connect FragPipe to a MSFragger .jar program file. If you already have such a file downloaded, use the 'Browse' button to select it or 'Update' to upgrade to the latest version. If you have not downloaded MSFragger before, use the 'Download' button. [(MSFragger installation help)](http://msfragger.nesvilab.org/tutorial_setup_fragpipe.html#install-update-or-use-an-already-downloaded-version-of-msfragger)
2. Connect FragPipe to a Philosopher program file. If you already have it downloaded, select 'Browse', otherwise select 'Download'. [(Philosopher installation help)](http://msfragger.nesvilab.org/tutorial_setup_fragpipe.html#install-update-or-use-an-already-downloaded-version-of-philosopher)
3. Optional: Python is needed to perform database splitting (necessary in complex searches/low memory situations) and spectral library generation. If you already have Python 3 or greater plus a few additional packages installed (**numpy**, **pandas**, **Cython**, and **msproteomicstools**) use 'Browse' to locate your python.exe file. [(Python installation help)](https://msfragger.nesvilab.org/tutorial_setup_fragpipe.html#optional-install-update-or-use-an-already-installed-version-of-python) 

For more help, see the full [tutorial on FragPipe configuration](https://msfragger.nesvilab.org/tutorial_setup_fragpipe.html).

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/fragpipe_1.png)
 

 <br>

#### Add input files:
In the next tab, 'Select LC/MS Files', drag & drop LC/MS files into the window or select 'Add files' or 'Add Folder Recursively' (to add all files in a folder, including those in subfolders).

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/fragpipe_2.png)

<br>
 
#### Group input files:
In the 'Select LC/MS Files' tab, indicate how you'd like PSM/peptide/protein reports to be generated.

##### For a single set of reports (search results from all input files merged)
Leave the 'Experiment' and 'Replicate' fields blank, and ensure that the 'Multi-Experiment Report' box on the 'Report' tab is not checked.

##### For reports with results from different replicates shown in separate columns
Indicate the 'Experiment' and 'Replicate' for each input file as shown below, where there are three replicates for two experimental conditions. On the 'Report' tab, check 'Multi-Experiment Report'. 
![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/specify_replicates.png)

##### For reports with results from different fractionated replicates shown in separate columns
Indicate the 'Experiment' and 'Replicate' for each input file as shown below, where each replicate (rep1, rep2) of two experimental conditions is composed of two fractions. Different fractions (1 & 2) from the same sample should have the same 'Experiment'/'Replicate' name. On the 'Report' tab, check 'Multi-Experiment Report'.
![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/specify_fractions.png)
<br>

**Note:** for compatibility with REPRINT ([Resource for Evaluation of Protein Interaction Networks](https://reprint-apms.org/)), 'Experiment' names should be written as `gene_condition`, e.g. `HDAC8_control`.
 <br>

 
#### Specify a protein sequence database:
In the 'Database' tab,

If you haven't made a database file using FragPipe/Philosopher before, select 'Download' to fetch one from Uniprot. Then choose your options and select an organism (use the uniprot proteome ID to specify your own, e.g. 'UP000000625' for E. coli).

Use 'Browse' to select a FASTA file from a previous FragPipe/Philosopher analysis.

If you need to use a custom FASTA database, it must follow a certain format and contain decoy sequences. Click 'Browse' to navigate to your custom FASTA. If you select 'Try Auto-Detect', 50% of the entries should contain the decoy tag. For help adding decoys and database formatting, see the instructions on the 'Database' tab or [here](https://github.com/Nesvilab/philosopher/wiki/Database).

  
![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/fragpipe_3.png)


 <br>

#### Set MSFragger search parameters:
In the 'MSFragger' tab,
1. Select the type of database search you want to perform.

   **Closed search**: To perform a closed search (normal precursor mass tolerance), select 'Closed Search'. This will prompt you to also update the downstream parameters for closed searching, select 'Yes'.

   **Open search**: To perform an open search (large precursor mass tolerance, used for finding unspecified post translational modifications), select 'Open Search'. This will prompt you to also update the downstream parameters for open searching, select 'Yes'.

   **Non-specific search**: To perform a closed search where peptides are not required to have any enzymatic terminus, select 'Non-specific Search'. This will prompt you to also update the downstream parameters for non-specific search, select 'Yes'. 
   
**Note:** For non-specific searches or for searches with many variable modifications, you may need to use the database splitting option, which will require 
   
 2. Fill in the amount of memory (in GB) that FragPipe will be allowed to use. We recommend at least 8-16 GB, but complex closed searches and open searches will require more.
 3. Specify the search parameters you want to use. For more information on these parameters, see the [MSFragger wiki page](https://github.com/Nesvilab/MSFragger/wiki/Setting-the-Parameters).
 
![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/fragpipe_4.png)
 
 
 <br>

#### Set downstream processing parameters:
In the 'Downstream' tab,
1. Select 'Run PeptideProphet' to validate your search results. (More information about PeptideProphet can be found [here](http://peptideprophet.sourceforge.net/).
2. If you previously updated the downstream parameters when setting MSFragger search parameters, you can skip to the next section. You can also re-load default downstream processing parameters by selecting the appropriate 'Load defaults' button.
3. Select 'Run ProteinProphet' to validate your protein identifications. (More information about ProteinProphet [here](http://proteinprophet.sourceforge.net/)).
4. If you are performing an open search, select [Crystal-C](https://www.nesvilab.org/Crystal-C/) to further improve filtering and interpretability of your results.

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/fragpipe_5.png)


 <br>
 
#### Specify filtering criteria and reports:
In the 'Report' tab,
1. Select 'Create report' to output tab-delimited tables of the search results.
2. Select 'Run Quantitation' to perform label-free quantification if desired.
3. If you are performing an open search, select 'Run PTMShepherd' to perform additional modification analysis.
4. Select 'Generate Spectral Library from search results' to generate spectral library if desired.

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/fragpipe_6.png)


 <br>
 
#### Run FragPipe:
1. Browse for the folder where you would like the search results to be written.
2. The 'Print Commands' button can be used to see every line of commands that will be executed without actually running them.
3. Press 'RUN' to begin the analysis! See the MSFragger [wiki](https://github.com/Nesvilab/MSFragger/wiki), [FAQ](https://github.com/Nesvilab/MSFragger/wiki/Frequently-Asked-Questions), and previous questions on [Github](https://github.com/Nesvilab/FragPipe/issues?utf8=%E2%9C%93&q=) for help.


![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/fragpipe_7.png)
 

