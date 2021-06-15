<div align="center">
<img src="images/msfragger-logo.png" width="350px"/>
</div>

MSFragger is an ultrafast database search tool for peptide identification in mass spectrometry-based proteomics. It has demonstrated excellent performance across a wide range of datasets and applications. MSFragger is suitable for standard shotgun proteomics analyses as well as large datasets (including timsTOF PASEF data), enzyme unconstrained searches (e.g., peptidome), open database searches (e.g., precursor mass tolerance set to hundreds of Daltons) for identification of modified peptides, and glycopeptide identification (N-linked and O-linked).  

MSFragger is implemented in the cross-platform Java programming language and can be used three different ways:

1. With [FragPipe](https://fragpipe.nesvilab.org) user interface
2. As a standalone Java executable, which we recommend using with [Philosopher](https://philosopher.nesvilab.org/) pipeline
3. Through [ProteomeDiscoverer](https://www.nesvilab.org/PD-Nodes/)

MSFragger writes peptide-spectrum matches in either tabular or pepXML formats, making it fully compatible with downstream data analysis pipelines such as Trans-Proteomic Pipeline and [Philosopher](https://nesvilab.github.io/philosopher/).  See the [complete documentation](https://github.com/Nesvilab/MSFragger/wiki), including a list of [Frequently Asked Questions](https://github.com/Nesvilab/MSFragger/wiki/Frequently-Asked-Questions). Example parameter files can be found [here](https://github.com/Nesvilab/MSFragger/tree/master/parameter_files).

### Supported file formats
The following spectral file formats can be searched directly with MSFragger, see the [FragPipe homepage](https://fragpipe.nesvilab.org/) for compatibility with workflow components downstream from MSFragger.

* mzML/mzXML - data from any instrument in mzML/mzXML format can be used

* Thermo RAW - Thermo raw files (.raw) can be read directly, conversion to mzML is not required

* Bruker timsTOF PASEF - MSFragger can read Bruker timsTOF PASEF (DDA) raw files (.d) directly, as well as MGF files converted by the Bruker DataAnalysis program. **Please note**: timsTOF data requires [Visual C++ Redistributable for Visual Studio 2017](https://aka.ms/vs/16/release/VC_redist.x64.exe) in Windows. If you see an error saying cannot find Bruker native library, please try to install the Visual C++ redistibutable.

### Download MSFragger 
Whether you run use FragPipe, PD, or the command line, you will need to download the latest MSFragger JAR file. See instructions for [downloading or upgrading MSFragger](https://github.com/Nesvilab/MSFragger/wiki/Preparing-MSFragger#Downloading-MSFragger).

### Release Notes
The latest version of MSFragger was released on 2021-03-09.
Check [here](CHANGELOG.md) for the full list of MSFragger versions and changes.

### Running MSFragger

#### FragPipe
On Windows or Linux, the easiest way to run MSFragger is through [FragPipe](https://fragpipe.nesvilab.org), which has a variety of built-in workflows for complete data analysis. 

#### Philosopher pipeline
Complete command line analyses can be performed with Philosopher, see this [tutorial](https://github.com/Nesvilab/philosopher/wiki/Simple-Data-Analysis) for a step-by-step example.

#### ProteomeDiscoverer node
MSFragger and Philosopher (PeptideProphet) are also available as processing nodes in Proteome Discoverer (PD, Thermo Scientific). Currently, the [MSFragger-PD node](https://www.nesvilab.org/PD-Nodes/) can be used in PD versions 2.2, 2.3 and 2.4.

#### Command line
See [Launching MSFragger](https://github.com/Nesvilab/MSFragger/wiki/Launching-MSFragger) on the Wiki page.

### Documentation
For technical documentation on MSFragger (hardware requirements, search parameters, etc.), see the [MSFragger wiki page](https://github.com/Nesvilab/MSFragger/wiki).

### Questions and Technical Support
See our [Frequently Asked Questions (FAQ)](https://github.com/Nesvilab/MSFragger/wiki/Frequently-Asked-Questions) page.
Please post all questions/bug reports regarding MSFragger itself on the [MSFragger GitHub page](https://github.com/Nesvilab/MSFragger), or if more appropriate on [FragPipe page](https://github.com/Nesvilab/FragPipe) or [Philosopher page](https://github.com/Nesvilab/philosopher).

### Requests for Collaboration
If you would like to propose a new collaboration that can take advantage of MSFragger and related tools, please contact us directly. 

### How to Cite
- Kong, A. T., Leprevost, F. V., Avtonomov, D. M., Mellacheruvu, D., & Nesvizhskii, A. I. (2017). MSFragger: ultrafast and comprehensive peptide identification in mass spectrometry–based proteomics. Nature Methods, 14(5), 513-520.
- Yu, F., Teo, G. C., Kong, A. T., Haynes, S. E., Avtonomov, D. M., Geiszler, D. J., & Nesvizhskii, A. I. (2020). Identification of modified peptides using localization-aware open search. Nature Communications, 11(1), 1-9.
- Polasky, D. A., Yu, F., Teo, G. C., & Nesvizhskii, A. I. (2020). Fast and Comprehensive N-and O-glycoproteomics analysis with MSFragger-Glyco. Nature Methods, 17, 1125-1132.

For other tools developed by the Nesvizhskii lab, see our website [www.nesvilab.org](http://www.nesvilab.org)
