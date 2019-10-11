## Performing a database search with FragPipe

##### FragPipe can be downloaded [here](https://github.com/Nesvilab/FragPipe/releases). Follow the instructions on that same Releases page to launch the program.

#### Configure FragPipe:
When FragPipe launches, the first tab in the window ('Config') will be used to configure the program.
1. Connect FragPipe to a MSFragger .jar program file. If you already have such a file downloaded, use the 'Browse' button to select it or 'Update' to upgrade to the latest version. If you have not downloaded MSFragger before, use the 'Download' button.
2. Connect FragPipe to a Philosopher program file. If you already have it downloaded, select 'Browse', otherwise select 'Download'.
3. Python is needed to perform database splitting (necessary in large database situation) and spectral library generation. We recommend you install version 3.7 or later [here](https://www.python.org/downloads/). Also install the following Python packages: **numpy**, **pandas**, **Cython**, **msproteomicstools** (only needed for spectral library generation).

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/fragpipe_1.png)
 

 <br>

#### Specify input files:
In the next tab, 'Select LC/MS Files',
1. Drag & drop LC/MS files into the window or select 'Add files' or 'Add Folder Recursively' (to add all files in a folder, including those in subfolders). If you have multiple fractions or experimental groups, specify the Experiment/Group for each file. Each unique identifier will have its own column in the resulting combined peptide & protein reports. Experimental conditions should be separated from the replicate number with an underscore ('\_'). Shown here are two experimental conditions (A, B) with three replicates each (1-3). The same identifier can be specified for multiple fractions belonging to the same sample. If no Experiment/Group identifiers are given, only one PSM/peptide/protein report will be generated.

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/fragpipe_2.png)
 

 <br>

 
#### Specify a protein sequence database:
In the 'Database' tab,
1. 'Browse' for the FASTA sequence database file that you want to use in the search, or select 'Download' to fetch one from Uniprot. The FASTA file must contain decoy sequences. For help adding decoys and database formatting, see [this page](https://github.com/Nesvilab/philosopher/wiki/Database).
2. Make sure the decoy prefix tag in the sequence database file is correct (necessary for target/decoy validation of identifications). If you select 'Try Auto-Detect', 50% of the entries should contain the decoy tag.
  
![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/fragpipe_3.png)


 <br>

#### Set MSFragger search parameters:
In the 'MSFragger' tab,
1. Select the type of database search you want to perform.

   **Closed search**: To perform a closed search (normal precursor mass tolerance), select 'Closed Search'. This will prompt you to also update the downstream parameters for closed searching, select 'Yes'.

   **Open search**: To perform an open search (large precursor mass tolerance, used for finding unspecified post translational modifications), select 'Open Search'. This will prompt you to also update the downstream parameters for open searching, select 'Yes'.

   **Non-specific search**: To perform a closed search where peptides are not required to have any enzymatic terminus, select 'Non-specific Search'. This will prompt you to also update the downstream parameters for non-specific search, select 'Yes'.
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
 

