### Offset search for PTMs with FragPipe
Parthenolide is a protein-reactive compound frequently used by cytoskeleton researchers to inhibit tubulin detyrosinases, but it is suspected to hit more than just those enzymes. Labeled peptides should have a +248.14125 Da mass shift, and we want to allow modification of any amino acid so we can learn more about parthenolide's specificity. This is a case for mass offset search.

The samples we will use for this tutorial are purified tubulin treated with either DMSO (control) or parthenolide. Citation: Hotta, Takashi, et al. "Parthenolide Destabilizes Microtubules by Covalently Modifying Tubulin." Current Biology 31.4 (2021): 900-907.



##### Tutorial contents
* [Add the data](https://msfragger.nesvilab.org/tutorial_offset.html#add-the-data)
* [Load the offset workflow](https://msfragger.nesvilab.org/tutorial_offset.html#load-the-offset-workflow)
* [Fetch a sequence database](https://msfragger.nesvilab.org/tutorial_offset.html#fetch-a-sequence-database)
* [Customize the search settings](https://msfragger.nesvilab.org/tutorial_offset.html#customize-the-search-settings)
* [Set the output location and run](https://msfragger.nesvilab.org/tutorial_offset.html#set-the-output-location-and-run)
* [Examine the results](https://msfragger.nesvilab.org/tutorial_offset.html#examine-the-results)

<br>

### Open FragPipe
When you launch FragPipe, check that MSFragger and Philosopher are both configured. If you haven’t downloaded them yet, use their respective ‘Download / Update’ buttons. See [this page](https://msfragger.nesvilab.org/tutorial_setup_fragpipe.html) for more help, Python is not needed for this exercise.

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/lfq-config.PNG)

<br>

### Add the data
1. Load the files (drag and drop or browse) and specify experiments: “DMSO” for the file ending 70, “PTL” (short for parthenolide) for the one ending 69.
2. Select the 'Mass-Offset-CommonPTMs' workflow from the dropdown menu and click 'Load'.

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/offset-workflow.png)

<br>

### Fetch a sequence database
3. Now we need to select a protein sequence database. You can choose to download a readymade human .fas file from [here](https://www.dropbox.com/s/v8tlkwu96f3txfj/2021-05-07-decoys-reviewed-contam-UP000005640.fas?dl=0), or you can download one using FragPipe. Downloading is easy, so we could also choose to download one at this point. On the Database tab, click the ‘Download’ button. Follow the prompts to use the default settings (reviewed human sequences with common contaminants).

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/lfq-databaseoptions.png)

Click ‘Yes’ to download the database. When it’s finished, you should see that the `FASTA file path` now points to the new database.


<br>

### Customize the search settings
4. In the MSFragger tab, check the first box in the Variable modifications section to set methionine oxidation as a variable modification. Because we want to allow parthenolide to label any residue (and because cysteines were alkylated after parthenolide was added), we need to make cysteine carbamidomethylation a variable mod instead of a fixed mod. To do this, first add C +57.02146 to the list of variable modifications.

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/offset-search.png)

5. Then scroll down to set fixed Mass Delta to 0 for cysteine.
6. When we loaded the 'Mass-Offset-CommonPTMs' workflow, the [default list of offsets](https://msfragger.nesvilab.org/common_mass_offsets.html) includes more than we need for this analysis since we want to focus on parthenolide. In the 'Mass Offsets' field, replace the offsets list with just 0/248.14125 for the parthenolide adduct.

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/offset-database1.png)

7. On the 'PTMs' tab, remove ‘Failed_Carbamidomethylation:-57.021464’ from the Custom mass shifts box (so that it is empty).

<br>

### Set the output location and run
8. On the Run tab, make a new folder for the output files (e.g. ‘offset_results’), then click ‘RUN’ and wait for the analysis to finish.

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/open-run.png)


When the run is finished, ‘DONE’ will be printed at the end of the text in the console.

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/tmt-2plexes-done.png)

<br>

### Examine the results
In the output location (‘offset_results’ folder), you will see subfolders containing individual results for DMSO and PTL, plus PTM-Shepherd output files that summarize the mass shifts from both experimental conditions together. A guide to all the output files can be found [here](https://msfragger.nesvilab.org/tutorial_fragpipe_outputs.html).

<br>
<br>
<br>
<br>

#### [Back to FragPipe homepage](https://fragpipe.nesvilab.org/)
