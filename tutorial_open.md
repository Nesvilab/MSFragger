### Open search for PTM discovery with FragPipe

One common use for open searches is finding experimental artifacts that can be included in subsequent closed searches to increase proteome coverage. Many sample preparation methods can modify peptides and reduce the likelihood of recovering them in a typical search. One such protocol is formalin-fixed paraffin-embedding (FFPE), a widely used tissue preservation method. There are a few different modification palettes that have been suggested in the literature (Metz et al., J. Biol. Chem., 2004; Hood et al., Mol. Cell. Proteom., 2005; Zhang et al., Proteomics, 2015) and we are interested in knowing which of these modifications, if any, are most relevant to our data.

For this tutorial, we will use one spectral file (2014-03-14\_-\_NSN\_-\_38B\_-\_2.mzML) from an FFPE-preserved sample of amyloid deposits in eye tissues, acquired on a SCIEX TripleTOF, originally in .raw format that has been [converted to .mzML by ProteoWizard](https://msfragger.nesvilab.org/tutorial_convert.html). (Publication: Nielsen, Nadia Sukusu, et al. "Insight into the protein composition of immunoglobulin light chain deposits of eyelid, orbital and conjunctival amyloidosis." Journal of proteomics & bioinformatics (2014).)


##### Tutorial contents
* [Open FragPipe](https://msfragger.nesvilab.org/tutorial_lfq.html#open-fragpipe)
* [Add the data](https://msfragger.nesvilab.org/tutorial_open.html#add-the-data)
* [Load the Open workflow](https://msfragger.nesvilab.org/tutorial_open.html#load-the-open-workflow)
* [Fetch a sequence database](https://msfragger.nesvilab.org/tutorial_open.html#fetch-a-sequence-database)
* [Inspect the search settings](https://msfragger.nesvilab.org/tutorial_open.html#inspect-the-search-settings)
* [Set the output location and run](https://msfragger.nesvilab.org/tutorial_open.html#set-the-output-location-and-run)
* [Examine the results](https://msfragger.nesvilab.org/tutorial_open.html#examine-the-results)


<br>

We will use a dataset (PRIDE/ProteomeXchange identifier PXD020556) in which HCT116 cells were treated with aspirin (acetylsalicylic acid) to investigate metabolic changes. Extracts from willows and other plants rich in acetylsalicylic acid have been used medicinally since Mesopotamian times. This tutorial will use a subset of the data to quantify the proteomes of aspirin treated and untreated (control) cells. These data were acquired with a Q Exactive HF-X.

Associated publication: Castoldi, Francesca, et al. "Autophagy-mediated metabolic effects of aspirin." Cell death discovery 6.1 (2020): 1-17.

To get the input data, download the 'lfq-raw.zip' file from [Dropbox](https://www.dropbox.com/sh/azdbblag7whv9v7/AACk8t4-6LowMYobKyXxUMS8a?dl=0) and extract the files.


### Open FragPipe
When you launch FragPipe, check that 
1. MSFragger and 
2. Philosopher
are both configured. If you haven’t downloaded them yet, use their respective ‘Download / Update’ buttons. See [this page](https://msfragger.nesvilab.org/tutorial_setup_fragpipe.html) for more help, Python is not needed for this exercise.

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/open-config.png)

<br>

### Add the data
3. On the Workflow tab, drag and drop the file 2014-03-14\_-\_NSN\_-\_36B\_-\_2.mzML file from the FFPE folder. Since we are only analyzing a single file, we don’t need to provide experiment or replicate labels.

### Load the Open workflow
4. Fragpipe includes built-in workflows for many common analyses. It is recommended to use the default workflows as a starting point for any custom analyses. Since we will be doing an open search, select the ‘Open’ workflow from the dropdown menu at the top of the page. Click ‘Load’ to configure FragPipe to run a complete open search workflow.

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/open-workflow.png)

<br>

### Fetch a sequence database
5. Now we need to select a protein sequence database. You can choose to download a readymade human .fas file from [here](https://www.dropbox.com/s/v8tlkwu96f3txfj/2021-05-07-decoys-reviewed-contam-UP000005640.fas?dl=0), or you can download one using FragPipe. Downloading is easy, so we could also choose to download one at this point. On the Database tab, click the ‘Download’ button. Follow the prompts to use the default settings (reviewed human sequences with common contaminants).

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/lfq-databaseoptions.png)

Click ‘Yes’ to download the database. When it’s finished, you should see that the `FASTA file path` now points to the new database.


<br>

### Inspect the search settings
6. On the MSFragger tab, have a look at the search parameters we will use. Note that a wide precursor mass tolerance is set, from -150 Da to +500 Da. In the Protein Digestion section, change the number of allowed missed cleavages from 2 to 1.

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/open-search.png)

<br>

### Set the output location and run
7. By loading the workflow, all other tabs have already been configured for a basic open search analysis, so skip to the Run tab to set the output location (a new folder called ‘my_FFPE_results’), then click ‘RUN’ and wait for the results.

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/open-run.png)


When the run is finished, ‘DONE’ will be printed at the end of the text in the console.

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/tmt-2plexes-done.png)

<br>

### Examine the results
In the output location (‘my_FFPE_results’ folder), you will find the results of the analysis. A guide to all the output files can be found [here](https://msfragger.nesvilab.org/tutorial_fragpipe_outputs.html).

In the 'my_FFPE_results' folder, you will see PTM-Shepherd output files (‘global.profile’ and ‘global.modsummary’) that help interpret all the mass shifts identified from the open search. Open the 'global.profile.tsv' file (in Excel or similar) to inspect it.

This file summarizes the mass shifts detected from all the FDR-filtered peptide-spectrum matches, sorted from most to least prominent. The contents of each column is described [here](https://msfragger.nesvilab.org/tutorial_fragpipe_outputs.html#globalprofiletsv).

<br>
<br>
<br>
<br>

#### [Back to FragPipe homepage](https://fragpipe.nesvilab.org/)
