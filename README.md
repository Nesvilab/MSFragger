# MSFragger

MSFragger is an ultrafast database search tool for peptide identification in mass spectrometry-based proteomics. It has demonstrated excellent performance across a wide range of datasets and applications. The speed of MSFragger makes it particularly suitable for the analysis of large datasets (including timsTOF data), for enzyme unconstrained searches, and for ‘open’ database searches (with the precursor mass tolerance set to hundreds of Daltons) for identification of modified peptides.

MSFragger is implemented in the cross-platform Java programming language, and can be used three different ways:

1. With [FragPipe GUI](https://fragpipe.nesvilab.org) (Graphical User Interface)
2. Through [ProteomeDiscoverer](https://www.nesvilab.org/PD-Nodes/)
3. As a standalone Java executable (JAR) file

MSFragger writes output in either tabular or pepXML formats, making it fully compatible with downstream data analysis pipelines such as Trans-Proteomic Pipeline and [Philosopher](https://nesvilab.github.io/philosopher/).  See the [complete documentation](https://github.com/Nesvilab/MSFragger/wiki), including a list of [Frequently Asked Questions](https://github.com/Nesvilab/MSFragger/wiki/Frequently-Asked-Questions). Example parameter files can be found [here](https://github.com/Nesvilab/MSFragger/tree/master/parameter_files).

## Supported instruments and file formats  
**mzML/mzXML**: Data from any instrument in mzML/mzXML format can be used.

**Thermo RAW**: MSFragger supports direct reading Thermo RAW files. MSFragger ProteomeDiscoverer (PD) node is fully compatible with all downstream PD tools. FragPipe has limited support for RAW files (no MS1-based label-free quantification); conversion to mzML when running FragPipe is recommended.      

**Bruker TimsTOF**: MSFragger support direct reading from Bruker timsTOF raw files (.d folder) and MGF files converted by Bruker DataAnalysis. Note that FragPipe currently has limited support for timsTOF data (no MS1-based label-free quantification yet). 

## Download MSFragger 
Whether you run it through FragPipe, PD, or stand-alone, you will need to download the latest MSFragger JAR file. See instructions for [downloading or upgrading MSFragger](https://github.com/Nesvilab/MSFragger/wiki/Preparing-MSFragger#Downloading-MSFragger).

## Release Notes
The latest version of MSFragger was released on 2019-09-08.
Check [here](CHANGELOG.md) for the full list of MSFragger versions and changes.

## Running MSFragger
<img src="images/4.jpg" width="300px" hspace="3px" align="right"/>

### FragPipe
On Windows, the easiest way to run MSFragger is using [FragPipe GUI](https://fragpipe.nesvilab.org). A tutorial on how to convert Thermo RAW files to mzML/mzXML (recommended for Thermo data to ensure full FragPipe functionality) can be found [here](tutorial_convert.md). FragPipe tutorial can be found [here](tutorial_fragpipe.md). 

FragPipe includes post-database search tool Philosopher (for downstream analysis with PeptideProphet and ProteinProphet), label-free quantification, FDR filtering, and report generation (at the PSM/ion/peptide/protein-levels). Additional tools (currently supporting Thermo data in mzML/mzXML format only) include DIA-Umpire SE module for DIA data, PTM-Shepherd for generating global PTM profiles, and SpectraST-based spectral library building module.  

### ProteomeDiscoverer node
<img src="https://raw.githubusercontent.com/Nesvilab/PD-Nodes/master/fig3.png" width="200px" hspace="3px" align="right"/>
MSFragger and Philosopher (PeptideProphet) are also available as processing nodes in Proteome Discoverer (PD, Thermo Scientific). Currently, the MSFragger-PD node can be used in PD v2.2 and v2.3.

Please visit our [PD-Nodes page](https://www.nesvilab.org/PD-Nodes/) for more information.
<br><br><br><br>

### Command line
See the [Launching MSFragger](https://github.com/Nesvilab/MSFragger/wiki/Launching-MSFragger) section of the Wiki page.


### Philosopher pipeline
Complete analyses can be performed with the Philosopher pipeline, a command line tool: [Tutorial](https://github.com/Nesvilab/philosopher/wiki/Processing-Filtering-and-Analyzing-Open-Search-Results-Using-Philosopher).

## Documentation
For documentation on MSFragger (hardware requirements, search parameters, etc.), see MSFragger [Documentation Wiki page](https://github.com/Nesvilab/MSFragger/wiki).  

## Questions and Technical Support
Please post all questions/bug reports regarding MSFragger itself on the [MSFragger GitHub page](https://github.com/Nesvilab/MSFragger), or if more appropriate on [FragPipe page](https://github.com/Nesvilab/FragPipe) or [Philosopher page](https://github.com/Nesvilab/philosopher).

## Requests for Collaboration
If you would like to propose a new collaboration that can take advantage of MSFragger and related tools, please contact us directly. 

## How to Cite
Kong AT, Leprevost FV, Avtonomov DM, Mellacheruvu D, Nesvizhskii AI. MSFragger: ultrafast and comprehensive peptide identification in mass spectrometry-based proteomics. Nature Methods 14:513–520 (2017). [Manuscript](https://www.nature.com/articles/nmeth.4256). 

For other tools developed by the Nesvizhskii lab, see our website [www.nesvilab.org](http://www.nesvilab.org)
