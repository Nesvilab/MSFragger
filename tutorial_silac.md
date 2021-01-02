## Analyzing SILAC labelled (or other chemical labelled) sample with FragPipe

[MSFragger](https://msfragger.nesvilab.org/) can be used to identify peptides with chemical labelling.

[IonQuant](https://ionquant.nesvilab.org/) inside FragPipe can be used to quantify chemical labelled (e.g. SILAC and dimethyl) samples.

Following is a step-by-step instruction. Please refer to other tutorials from [here](https://fragpipe.nesvilab.org/) for the basic knowledge of using FragPipe.


### Load `Default` workflow
Explanations of the build-in workflows can be found from [here](https://msfragger.nesvilab.org/tutorial_fragpipe_workflows.html)

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/silac_1.jpg)


### Specify or download FASTA file
![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/silac_2.jpg)


### Select the right variable modifications
Following are variable modifications for SILAC. If you are using other kind of chemical labelling, please fill in the right sites and masses.

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/silac_3.jpg)


### Use IonQuant in MS1 quantification
Check `Run MS1 quant` and load the default settings. Then fill in the labels masses. The format is `<site>mass`, and there can be multiple site-mass pairs.

Following is an example of SILAC light, medium, and high labelling.

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/silac_4.jpg)


### Specify output folder and run
![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/silac_5.jpg)


## Output
Each experiment have a folder containing various files. Among them `psm.tsv`, `ion.tsv`, `peptide.tsv`, and `protein.tsv` files that are human readable and can be used for downstream analysis. Entries in these files have been filtered with user defined FDR threshold. The chemical labels are shown as variable modifications.

There are also two files designed for chemical labelling exclusively: `ion_label_quant.tsv` and `peptide_label_quant.tsv`. Entries in these two files are paired light and heavy peptides/ions.

