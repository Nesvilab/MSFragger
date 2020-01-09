## Importing MSFragger results from PASEF data into Skyline

##### This tutorial covers spectral library building in Skyline from validated MSFragger search results of Bruker TIMS-TOF PASEF data. We used Skyline-daily (v 19.1.9.350) and two files from the dataset published by [Meier et al](https://www.mcponline.org/content/early/2018/11/01/mcp.TIR118.000900), which can be downloaded from [ProteomeXchange](http://proteomecentral.proteomexchange.org/cgi/GetDataset?ID=PXD010012) (`HeLa_200ng_100ms_raw.zip` on the FTP site).

#### Set up the analysis
Make sure the PeptideProphet output files ('interact-pep.xml'), raw spectral files ('.d'), and .mgf files ('.mgf' or '\_calibrated.mgf') in the same directory or in the same parent directory. You will also need the protein sequence database filtered at 1% FDR which is output from Philosopher ('protein.fas') that you used in the search.

#### Create a new DDA document

Launch Skyline and select **'Import DDA Peptide Search'** from the Start Page. Follow the prompts to choose a name and location for the new document to be saved.

#### Import peptide results
Once the new document is saved, **'Add Files'** to select the 'interact-pep.xml' files for the search results you want to import. To generate a spectral library that is filtered to 1% ion FDR and 1% protein FDR, we recommend specifying the peptide probability threshold that corresponds to 1% ion FDR. (This can be found in the FragPipe log or .log file, the value 0.8437 would be used in this example:
_INFO[15:56:39] Converged to 0.08 % FDR with 57671 Ions       decoy=51 threshold=**0.8437** total=57722_)


Then press **'Next'**, prompting Skyline to build the spectral library from these peptide search results.

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/Skyline_PASEF_4.png)

#### Add spectral files
When the spectral library is built, Skyline should automatically detect the spectral files. Press **'Next'**. If Skyline detects that the files in your experiment are named with a common prefix, you have the option to shorten the result names at this point for easier comparison later on.

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/Skyline_PASEF_5.png)

#### Add detected modifications
Skyline should automatically detect variable modifications from your search results. Select the suggested modifications and press **'Next'**.

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/Skyline_PASEF_6.png)

#### Configure scan settings
Precursor charge states greater than 2 can be added at this point. Press **'Next'**.

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/Skyline_PASEF_7.png)

#### Add FASTA file
**'Browse'** for the sequence database, and select the number of missed cleavages that was used in the database search. Press **'Next'** to insert the 'protein.fas' file.

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/Skyline_PASEF_8.png)

#### Filter targets
When the FASTA file is finished importing, select the desired filters, and  press **'OK'** to start the import.

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/Skyline_PASEF_9.png)

#### Importing the results
The import will take a few minutes per file.

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/Skyline_PASEF_10.png)

#### View results
Once the import is finished, you are ready to perform your Skyline analyses, select a peptide from the list to view. Quantification can be compared between runs via _View > Peak Areas > Replicate Comparison_. 

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/Skyline_PASEF_12.png)

To see the two-dimensional ion mobility vs. m/z plot, click on the apex of the chromatogram.

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/Skyline_PASEF_13.png)


