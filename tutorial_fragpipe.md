# Performing a database search with FragPipe

#### FragPipe can be downloaded [here](https://github.com/Nesvilab/FragPipe/releases).
#### Follow the instructions on the same Releases page to launch the program. 

## Configure FragPipe:
When FragPipe launches, the first tab in the window ('Config') will be used to configure the program.
1) Connect FragPipe to a MSFragger .jar program file. If you already have such a file downloaded, use the 'Browse' button to select it or 'Update' to upgrade to the latest version. If you have not downloaded MSFragger before, use the 'Download' button.
2) Connect FragPipe to a Philosopher program file. If you already have it downloaded, select 'Browse', otherwise select 'Download'.
3) Python is needed to perform database splitting (necessary in most situations) and spectral library generation. We recommend you install version 3.7 or later [here](https://www.python.org/downloads/). Also install the following Python packages: **numpy**, **pandas**, **Cython**, **msproteomicstools**.

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/tutorial/images/1.jpg)
 

 <br>

## Specify input files:
In the next tab, 'Select LC/MS Files',
1) Drag & drop mzML files into the window or select 'Add files' or 'Add Folder Recursively' (to add all files in a folder, including those in subfolders).

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/tutorial/images/2.jpg)
 

 <br>

 
## Specify a protein sequence database:
In the 'Sequence DB' tab,
1) 'Browse' for the FASTA sequence database file that you want to use in the search, or select 'Download' to fetch one from Uniprot.
2) Make sure the decoy prefix tag in the sequence database file is correct (necessary for target/decoy validation of identifications). If you select 'Try Auto-Detect', 50% of the entries should contain the decoy tag.
  
![](https://raw.githubusercontent.com/Nesvilab/MSFragger/tutorial/images/3.jpg)


 <br>

## Set MSFragger search parameters:
1) Select the type of database search you want to perform.

   **Closed search**: To perform a closed search (normal precursor mass tolerance), select 'Closed Search'. This will prompt you to also update the downstream parameters for closed searching, select 'Yes'.

   **Open search**: To perform an open search (large precursor mass tolerance, used for finding unspecified posttranslational modifications), select 'Open Search'. This will prompt you to also update the downstream parameters for open searching, select 'Yes'.

   **Non-specific search**: To perform a closed search where peptides are only required to have one enzymatic terminus, select 'Non-specific Search'. This will prompt you to also update the downstream parameters for semispecific searching, select 'Yes'.
 2) Select the amount of memory (in GB) that FragPipe can use.
 3) Specify the search tolerances you want to use. For more information on these parameters, see the [MSFragger wiki page](https://github.com/Nesvilab/MSFragger/wiki).
 
![](https://raw.githubusercontent.com/Nesvilab/MSFragger/tutorial/images/5.jpg)
 
 
 <br>

## Set downstream processing parameters:
1) Select 'Run PeptideProphet' to validate your search results. (More information about PeptideProphet can be found [here](http://peptideprophet.sourceforge.net/).
2) If you previously updated the downstream parameters when setting MSFragger search parameters, you can skip to the next section. You can also re-load default downstream processing parameters by selecting the appropriate 'Load defaults' button.
3) Select 'Run ProteinProphet' to validate your protein identifications. (More information about ProteinProphet [here](http://proteinprophet.sourceforge.net/)).
4) If you want completely separate reports for each input file, leave this box unchecked and also select the 'Separate ProteinProphet' prot.xml file per group/experiment' option.
5) If you are performing an open search, select [Crystal-C](https://www.nesvilab.org/Crystal-C/) to further improve filtering and interpretability of your results.

**\! replace this image:**
![](https://raw.githubusercontent.com/Nesvilab/MSFragger/tutorial/images/6.jpg)


 <br>
 
## Specify filtering criteria and reports:
1) Select 'Create report' to output tab-delimited tables of the search results.
2) Select 'Label-free Quant' to perform label-free quantification. 
3) Optionally select 'Generate Spectral Library from search results'.

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/tutorial/images/7.jpg)


 <br>
 
## Run FragPipe:
1) Browse for the folder where you would like the search results to be written.
2) Press 'RUN' to begin the analysis!


![](https://raw.githubusercontent.com/Nesvilab/MSFragger/tutorial/images/8.jpg)
 

