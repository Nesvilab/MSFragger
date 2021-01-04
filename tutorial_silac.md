## Analyzing SILAC (or other labelling coupled with MS1-based quantification) samples with FragPipe

[MSFragger](https://msfragger.nesvilab.org/) can be used to identify labelled peptides.

[IonQuant](https://ionquant.nesvilab.org/) inside FragPipe can be used to perform MS1 quantification for labelled samples.

Following is a step-by-step instruction. Please refer to other tutorials from [here](https://fragpipe.nesvilab.org/) for the basic knowledge of using FragPipe.


### Load `Default` workflow
Explanations of the build-in workflows can be found from [here](https://msfragger.nesvilab.org/tutorial_fragpipe_workflows.html)

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/silac_1.jpg)


### Specify or download FASTA file
![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/silac_2.jpg)


### Select the right variable modifications
Following illustrates specification of variable modifications for SILAC.

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/silac_3.jpg)

If you are using other kind of labelling, please fill in the corresponding sites and modification masses. 

Taking light and heavy dimethyl labelling for example, the variable modification should be

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/silac_3_2.jpg)


### Use IonQuant for MS1 quantification
Check `Run MS1 quant` and load the default settings. Then fill in the labels' masses. The format is `<site>mass`, and there can be multiple site-mass pairs separated by `;`.

Following is an example of using SILAC light, medium, and heavy labelling.

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/silac_4.jpg)

If you are using light and heavy dimethyl labelling, please change these fields to

![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/silac_4_2.jpg)

### Specify output folder and run
![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/silac_5.jpg)


## Output
For each experiment, the results folder contains various files. As with any typical FragPipe analysis, among them are `psm.tsv`, `ion.tsv`, `peptide.tsv`, and `protein.tsv` files. Entries in these files have been filtered with user defined FDR threshold. The SILAC (or similar) modifications are shown as variable modifications. For SILAC (and similar) samples they may not be sufficient as they do not provide linked (Light/Heavy) abundances at each (ion/peptide/protein) level. Instead, as for label-free data, each PSM/ion/peptide is considered independently, and the protein file shows combined protein intensity based on all peptides, regardless of the label/sample status.   

Thus, for SILAC (and related) data, IonQuant has been extended to generate two additional files, designed for labelled data exclusively: `ion_label_quant.tsv` and `peptide_label_quant.tsv`. Entries in these two files correspond to those in 'ion.tsv' and 'peptide.tsv' files, respecively, but are presented in a paired (Light/Heavy) format. The users will likely find these two files more useful when analyzing SILAC data. At present, however, IonQuant does not generate a similar protein-level file (we are working to add a similar protein-level, paired quantification file in a future release of IonQuant).

