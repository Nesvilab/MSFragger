# Performing glycoproteomics searches with MSFragger-Glyco

## Contents
1. Getting Started
2. Glyco-search with MSFragger: Search Types and Parameters
3. Using FragPipe to run MSFragger glyco searches
4. Running MSFragger glyco searches from terminal/Linux

## 1) Getting Started

#### MSFragger can be downloaded [here](https://msfragger.nesvilab.org/)
#### FragPipe (a graphical interface and pipeline for MSFragger on Windows) can be downloaded [here](https://github.com/Nesvilab/FragPipe/releases). 
Follow the instructions on the FragPipe Releases page to launch the program. We recommend using 
FragPipe for Windows users. All parameters for running glyco searches detailed below can be 
found in the MSFragger tab of FragPipe, and detailed instructions for running glyco searches can 
be found in section (3) of this tutorial.  

#### System Requirements: 
Before you get started, make sure your LC-MS file format is compatible with the workflows you want to perform (for Thermo data, 
we recommend [converting .raw files to mzML](https://msfragger.nesvilab.org/tutorial_convert.html), for Bruker data, see this 
[tutorial](https://msfragger.nesvilab.org/tutorial_fragpipe_pasef.html)).      
See the main MSFragger wiki page [here](https://github.com/Nesvilab/MSFragger/wiki) for full details of system requirements. 
 

## 2) Glyco-search with MSFragger: Search Types and Parameters:

The types of searches that can be performed for glycoproteomics data are detailed below, along with several
key parameters and recommended settings. Details on all parameters can be found in the MSFragger documentation
[here](https://github.com/Nesvilab/MSFragger/wiki). The key parameters listed here are the differences required
to perform a glyco-search; all other parameters can generally be used as in a normal MSFragger search (i.e.
left as default or set to appropriate values for your instrument/analysis). Default parameter files for 
several types of glyco-searches can be found [here](https://github.com/Nesvilab/MSFragger/tree/master/parameter_files),
or by loading a glyco workflow in FragPipe. 

### Mass Offset Search

This is the primary search method recommended for glycoproteomics searches with MSFragger. It uses
involves setting glycan masses of interest as mass offsets (similar to an open search, but only considering
a narrow window around each mass offset). This allows MSFragger to simultaneously search for peptides that have lost none, 
part, or all of their original glycan, making it ideal for searching collisional, hybrid, and photo-activation datasets.    
**Key Parameters**:

1. **labile_search_mode**: *(possible values: nglycan, labile, off)* nglycan mode checks for N-glycosylation motif N-X-S/T (X is not P), but is otherwise identical to "labile" mode. Labile mode should be used for all labile modifications (other than N-glycans), including O-glycans. Specify the allowed residues in deltamass_allowed_residues. "Off" results in a standard (non-glyco) MSFragger search, in which all mass offsets are assumed to remain intact during activation.  
2. **deltamass_allowed_residues**: (used in "labile" mode ONLY). Specify which amino acids (single letter codes) are allowed to contain the glycan mass offsets. Default: ST (for O-glycoproteomics searches). NOT used in nglycan mode. 
3. **mass_offsets**: (value: 0/mass1/mass2/...) All possible glycan masses should be specified as mass offsets (separated by '/'). Depending on 
the type of data and search, the glycans considered can vary. The masses of all glycans of interest should be determined and converted to 
a list separated by '/' (see example parameter file). An arbitrary number of mass offsets can be searched, but search speed decreases with the 
number of masses used. If more than a few thousand masses are being considered (e.g. in an exploratory search), consider using an open search instead.
4. **fragment_ion_series**: fragments types of interest should be specified here depending on the activation method and data. b~/y~ refer to b/y ions + HexNAc (common for N-glycans in CID/HCD). Recommendations:   
**CID/HCD/IRMPD** - b,y,b~,y~,Y (NGlycan or low energy) or b,y,Y (OGlycan or high energy)  
**hybrid(EThcD/AIETD/etc)** - b,y,c,z,Y  
**ETD/ECD** - c,z  
5. **localize_delta_mass**: (values: 0 or 1) specifies whether to search for shifted ions (i.e. peptide fragments containing the intact glycan). Recommended (1) for ETD/ECD and hybrid searches (EThcD/AIETD/etc), not recommended (0) for CID/HCD/IRMPD.
6. **Y_type_masses**: (value: 0/mass1/mass2/...) Masses of Y-type ions (intact peptide plus partially fragmented glycan) to consider in search. Note that ALL Y masses are applied to ALL peptide searches, so including too many can reduce search performance. Can be used in non-glyco searches as well (any modification that partially fragments, leaving behind some mass can be considered). 
7. **diagnostic_fragments**: (value: mass1/mass2/...) m/z values of diagnostic fragment ions (e.g. Oxonium ions) that appear in spectra of peptides containing a mod of interest. If diagnostic_intensity_filter > 0, at least one of the masses provided here must be found at sufficient intensity for any mass offset to be searched for the spectrum. To disable this checking, change diagnostic_intensity_filter to 0.
8. **diagnostic_intensity_filter**: Minimum relative intensity (relative to base peak height) for the SUM of intensities of all diagnostic fragment ions found in the spectrum to consider this a potential glyco (or other labile mod) spectrum. Set to 0 to disable. A value of 0.1 means summed intensity must be 10% the height of the base peak in the MS/MS spectrum to be considered. 
9. **deisotope**: (values: 0, 1, or 2) glycopeptides tend to be larger than tryptic peptides, making deisotoping very helpful. Recommended setting 1 for glyco data. 

### Open Search

Open searches can be performed on glycoproteomics data, for example to determine what glycans are present in the data.
Open searches function similarly to the mass offset search in that delta masses (mass offsets) between precursor and sequence masses are used to define glycans
and other modifications, but with a few key differences. Because any mass shift (within the provided tolerance)
is allowed, not all mass shifts correspond to glycans. For this reason, **oxonium filtering is currently disabled for open searches**. 
However, glycopeptide-specific fragments ions (Y, b~, y~) can still be generated for peptides containing 
the sequon/residue(s) of interest to effectively search for glycopeptides. If glycans of interest are known, a mass offset 
search will likely be more sensitive.    
**Key Parameters**:

1. **labile_search_mode, fragment_ion_series, Y_type_masses, and deisotope** should be used as in mass offset glyco-searches (see above).
2. **localize_delta_mass**: shifted ions are not necessary for fully labile modifications (like glycosylation in CID/HCD searches), but can be useful for determining the presence of other types of modifications. 
If interested only in glycans, use the recommended settings for mass offset search; if interested in other modifications as well, set to 1. 
3. **mass_offsets, isotope_error**: set to 0
4. **precursor_mass_lower, precursor_mass_upper**: these define the range of the open search. For example, precursor_mass_lower = -200, precursor_mass_upper = 2500 would allow any mass shift between -200 and 2500 Da, accounting for many types of glycans (and many other peptide modifications). 
5. **deltamass_allowed_residues, diagnostic_fragments, and diagnostic_intensity_filter** are NOT yet supported for open searches. 

### Variable Modification Search
Recommended only for ETD/ECD data. Enter glycans of interest as variable modifications (see the
[MSFragger wiki](https://github.com/Nesvilab/MSFragger/wiki)
for formatting details) on specified residue(s). It is not recommended to search more than a dozen or so
modifications at once.  
**Key Parameters**:

1. **labile_search_mode**: . Variable modification searches should not be used for labile modifications (set to 'off'). If performing an ETD/ECD glyco-search, set to 'off' (*even though it is a glyco-search, the glycans are not labile in ETD/ECD*). If set to off, labile fragment ions (Y, b~,y~) will not be generated
2. **fragment_ion_series**: Y, b~, and y~ ion types are NOT recommended for ETD/ECD data (as they should not occur). All other ion types function as normal 
3. **mass_offsets**: not used. (mass_offsets = 0)


## 3) Performing a glycoproteomics search with FragPipe

#### FragPipe can be downloaded [here](https://github.com/Nesvilab/FragPipe/releases). Follow the instructions on that same Releases page to launch the program.

#### Please use the main FragPipe tutorial [here](https://github.com/Nesvilab/MSFragger/blob/master/tutorial_fragpipe.md) to learn the basics of FragPipe. This tutorial will cover only the differences needed for glycoproteomics searches from the basic workflow outlined there 

### Getting Started

FragPipe includes a number of pre-packaged **workflows**, including several for glycoproteomics
searches. We recommend using one of these workflows as a starting point, but parameters can be entered
 manually as well. 

#### To load a workflow:
![](https://github.com/Nesvilab/MSFragger/blob/master/images/Fragpipe-glyco_1.PNG)

Navigate to the workflow tab, select a glycoproteomics workflow from the dropdown menu, and press the "Load" button. All default glycoproteomics 
workflows begin with "glyco-", followed by the type of glycan (N-linked or O-linked), and activation
type (HCD or Hybrid). "HCD" is optimized for beam-type CID fragmentation but can be used as a starting point
for any vibrational activation (trap CID, IRMPD, etc). "Hybrid" refers to combined electronic (e.g. ETD) and
vibrational activation, for example, EThcD or ETciD. 

The workflow will initialize default parameters on several of the subsequent tabs.


### Editing glyco-relevant parameters

#### Database tab:
See the FragPipe tutorial for information on how to load a database file. No differences are present for glycoproteomics searches.


#### MSFragger tab:
The vast majority of differences between regular and glycoproteomics searches can be found on 
MSFragger tab. The key areas are highlighted here. Standard parameters are modified as in
a typical search - see the main FragPipe tutorial for details about the parameters on this page.
Open searches are performed by changing the precursor mass range and units here.      
![](https://github.com/Nesvilab/MSFragger/blob/master/images/Fragpipe-glyco_2.PNG)

##### Advanced parameters
![](https://github.com/Nesvilab/MSFragger/blob/master/images/Fragpipe-glyco_3.PNG)     
Most of the glyco-search options can be found in the advanced section. For mass offset glyco searches,
input all glycan masses of interest in the mass offset box **(1)**. Open searches leave this box empty.     
**(2)** Adjust the options in the Glyco/Labile mods box.
1. **Search Mode**: distinguishes between types of mass offset and open searches. Options are:    
	*nglycan*: for N-linked glycans. Uses consensus sequon N-X-S/T (X is not P) for glycosites    
	*labile*: for all other labile modifications, **including O-linked glycans**    
	*off*: for modifications that do not dissociate. Should not be used for glyco search.        
2. **Allowed Resides**: for **labile** search type **only**. Determines the allowed residues
for mass offsets to be considered. Input is single letter amino acid codes. For O-linked glycan searches, default is ST.      
3. **Diagnostic Ion Minimum Intensity**: Used to filter spectra considered for searching glycans
based on the presence of oxonium ions. If set to 0, filter will not be used. Otherwise, value is the
minimum for the summed relative intensity of all detected oxonium ions for the spectrum to be considered
 for glyco searching. Default value is 0.1, meaning that the sum of all oxonium ion intensities
 must be at least 10% of the base peak in the spectrum to pass the check.     
4. **Y ion masses**: If searching for Y ions (intact peptide with partial glycan), enter the list
of masses to use here. Masses should be the mass of sugar residues only, no charging proton or terminal groups. 
Note: these ions will be searched for ALL glycans, so keeping the list short
and including only ions that appear frequently will improve performance. *These values are only used*
*if "Y" is included in the fragment ion series (see below)*          
5. **Diagnostic Fragment Masses**: Enter masses of oxonium ions to search for potential glyco-spectra.
This list can include rare ions without negatively impacting performance. *Masses should be entered as the observed m/z value of the oxonium ion, i.e. [M+H]+*     
 
**(3)** Enter the fragment ion types appropriate to your analysis in the "Fragment ion series" box. Recommendations are as follows, but should be adjusted based 
the types of glycans being studied and/or acquisition parameters:     
**N-glycan CID/HCD**: b,y,b~,y~,Y      
**N-glycan hybrid (EThcD, etc)**: b,y,c,z,Y      
**O-glycan CID/HCD**: b,y      
**O-glycan hybrid (EThcD, etc)**: b,y,c,z      
**N- or O-glycan ETD/ECD**: c,z *(NOTE: this search should be done with glycans as variable modifications, NOT mass offsets, as glycans are not expected to dissociate in this mode.)*     

#### Validation tab:
For highly enriched N-glycopeptides (at least 10-20% of all spectra are of glycopeptides), setting the "--glyc" tag in the
PeptideProphet options can help by modeling peptides with the consensus sequon (N-X-S/T) separately from peptides without. 
Otherwise, there are no differences on this page between a glyco-search and a standard mass offset or open search. 

#### All other tabs:
No difference between a regular MSFragger search and a glyco search. See the main FragPipe tutorial linked
at the beginning of this document for details and instructions. 



## 4) Running MSFragger glyco searches from terminal/Linux
On Windows, we strongly recommend using FragPipe (above) to run MSFragger, but the linux commands below
can be adapted to run via command line if desired.  

On Linux, the following shell script includes commands to run MSFragger and downstream processing with Philosopher
for glyco-searches. These commands are identical to standard MSFragger operation, the only difference for
a glyco-search is in the MSFragger parameters file.  
 
**Changes from defaults**
- If you are searching N-glycans and have highly enriched data (at least ~20% of PSMs are glycopeptides), adding the --glyc tag in the PeptideProphet step can help
with modeling. 
- When using mass offset or open searches, make sure the --masswidth provided to PeptideProphet is large
enough to include the largest of your glycan masses (otherwise those PSMs will not be modeled). 

Linux shell script:

>\#!/bin/bash
>
>set -xe
>
>\# Specify paths of tools and files to be analyzed.  
>dataDirPath="data/"  
>fastaPath="2020-01-22-decoys-reviewed-contam-UP000005640.fas"  
>msfraggerPath="/fragger-dir/msfragger-2.5.jar"  
>fraggerParamsPath="fragger.params"  
>philosopherPath="/philosopher-dir/philosopher"  
>decoyPrefix="rev_"  
>
>\# Run MSFragger. Change the -Xmx value according to your computer's memory.  
>java -Xmx32G -jar $msfraggerPath $fraggerParamsPath $dataDirPath/<spectral files ending with .mzML (required for quantification) or .raw>
>
>\# Move pepXML files to current directory.  
>mv $dataDirPath/*.pepXML ./
>
>\# Move MSFragger tsv files to current directory.   
>mv $dataDirPath/*.tsv ./ # Comment this line if localize_delta_mass = 0 in your fragger.params file.
>
>\# Run PeptideProphet, ProteinProphet, and FDR filtering with Philosopher  
>$philosopherPath workspace --clean  
>$philosopherPath workspace --init  
>$philosopherPath database --annotate $fastaPath --prefix $decoyPrefix  
>
>\# Pick one from the following commands and comment the other.    
>$philosopherPath peptideprophet --nonparam --expectscore --decoyprobs --ppm --accmass --decoy $decoyPrefix --database $fastaPath ./\*.pepXML # closed search    
>$philosopherPath peptideprophet --nonparam --expectscore --decoyprobs --masswidth 4000.0 --clevel -2 --decoy $decoyPrefix --combine --database $fastaPath ./\*.pepXML # Open or Mass Offset search   
>
>$philosopherPath proteinprophet --maxppmdiff 20000000 ./\*.pep.xml
>
>\# Pick one from the following commands and comment the other one.  
>$philosopherPath filter --sequential --razor --mapmods --tag $decoyPrefix --pepxml ./ --protxml ./interact.prot.xml # closed or non-specific closed search  
>$philosopherPath filter --sequential --razor --mapmods --tag $decoyPrefix --pepxml ./interact.pep.xml --protxml ./interact.prot.xml # Open search  
>
>\# Perform quantification.  
>$philosopherPath freequant --dir $dataDirPath
>
>\# Make reports.  
>$philosopherPath report


