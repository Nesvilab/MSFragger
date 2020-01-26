# Running a FragPipe-equivalent workflow on Linux

Example shell scripts for TIMS-TOF PASEF data (with [IMQuant](https://github.com/Nesvilab/IMQuant)) and non-ion mobility data are shown below, modify them to suit your configuration.
<br>

### TIMS-TOF data:

```shell
#!/bin/bash

set -xe

# Specify paths of tools and files to be analyzed.
dataDirPath="data/"
fastaPath="2020-01-22-decoys-reviewed-contam-UP000005640.fas"
msfraggerPath="MSFragger-2.2.jar"
fraggerParamsPath="fragger.params"
philosopherPath="philosopher.2.0.0"
crystalcPath="CrystalC-1.0.5.jar"
crystalcParameterPath="crystalc.params"
decoyPrefix="rev_"

# Run MSFragger. Change the -Xmx value according to your computer's memory.
java -Xmx64G -jar $msfraggerPath $fraggerParamsPath $dataDirPath/<spectral files ending with .d>

# Move pepXML files to current directory.
mv $dataDirPath/*.pepXML ./

# Move MSFragger tsv files to current directory.
mv $dataDirPath/*.tsv ./ # Comment this line if localize_delta_mass = 0 in your fragger.params file.

# For open searches, run Crystal-C. Otherwise, don't run Crystal-C (comment this for-loop).
for myFile in ./*.pepXML
do
	java -Xmx64G -cp $crystalcPath Main $crystalcParameterPath $myFile
done

# Run PeptideProphet, ProteinProphet, and FDR filtering with Philosopher
$philosopherPath workspace --clean
$philosopherPath workspace --init
$philosopherPath database --annotate $fastaPath --prefix $decoyPrefix

# Pick one from the following three commands and comment the other two.
$philosopherPath peptideprophet --nonparam --expectscore --decoyprobs --ppm --accmass --decoy $decoyPrefix --database $fastaPath ./*.pepXML # Closed search
$philosopherPath peptideprophet --nonparam --expectscore --decoyprobs --masswidth 1000.0 --clevel -2 --decoy $decoyPrefix --combine --database $fastaPath ./*.pepXML # Open search
$philosopherPath peptideprophet --nonparam --expectscore --decoyprobs --ppm --accmass --nontt --decoy $decoyPrefix --database $fastaPath ./*.pepXML # Non-specific closed search

$philosopherPath proteinprophet --maxppmdiff 2000000 ./*.pep.xml

# Pick one from the following two commands and comment the other one.
$philosopherPath filter --sequential --razor --mapmods --tag $decoyPrefix --pepxml ./ --protxml ./interact.prot.xml # closed or non-specific closed search
$philosopherPath filter --sequential --razor --mapmods --tag $decoyPrefix --pepxml ./interact.pep.xml --protxml ./interact.prot.xml # Open search

# Run IMQuant. Change the -Xmx value according to your computer's memory.
java -Xmx64G -jar IMQuant.jar --psm <path to psm.tsv> <path to .d> <path to .pepXML>

# Make reports.
$philosopherPath report
$philosopherPath workspace --clean

```
**Please note: The [IMQuant.jar](https://github.com/Nesvilab/IMQuant/releases/latest) file must be in the same directory as the `ext` folder.** To see the IMQuant help, run `java -jar IMQuant.jar`.

<br>


### Non-ion mobility data:

```shell
#!/bin/bash

set -xe

# Specify paths of tools and files to be analyzed.
dataDirPath="data/"
fastaPath="2020-01-22-decoys-reviewed-contam-UP000005640.fas"
msfraggerPath="MSFragger-2.2.jar"
fraggerParamsPath="fragger.params"
philosopherPath="philosopher.2.0.0"
crystalcPath="CrystalC-1.0.5.jar"
crystalcParameterPath="crystalc.params"
decoyPrefix="rev_"

# Run MSFragger. Change the -Xmx value according to your computer's memory.
java -Xmx64G -jar $msfraggerPath $fraggerParamsPath $dataDirPath/<spectral files ending with .mzML (required for quantification) or .raw>

# Move pepXML files to current directory.
mv $dataDirPath/*.pepXML ./

# Move MSFragger tsv files to current directory.
mv $dataDirPath/*.tsv ./ # Comment this line if localize_delta_mass = 0 in your fragger.params file.

# For open searches, run Crystal-C. Otherwise, don't run Crystal-C (comment this for-loop).
for myFile in ./*.pepXML
do
	java -Xmx64G -cp $crystalcPath Main $crystalcParameterPath $myFile
done

# Run PeptideProphet, ProteinProphet, and FDR filtering with Philosopher
$philosopherPath workspace --clean
$philosopherPath workspace --init
$philosopherPath database --annotate $fastaPath --prefix $decoyPrefix

# Pick one from the following three commands and comment the other two.
$philosopherPath peptideprophet --nonparam --expectscore --decoyprobs --ppm --accmass --decoy $decoyPrefix --database $fastaPath ./*.pepXML # Closed search
$philosopherPath peptideprophet --nonparam --expectscore --decoyprobs --masswidth 1000.0 --clevel -2 --decoy $decoyPrefix --combine --database $fastaPath ./*.pepXML # Open search
$philosopherPath peptideprophet --nonparam --expectscore --decoyprobs --ppm --accmass --nontt --decoy $decoyPrefix --database $fastaPath ./*.pepXML # Non-specific closed search

$philosopherPath proteinprophet --maxppmdiff 2000000 ./*.pep.xml

# Pick one from the following two commands and comment the other one.
$philosopherPath filter --sequential --razor --mapmods --tag $decoyPrefix --pepxml ./ --protxml ./interact.prot.xml # closed or non-specific closed search
$philosopherPath filter --sequential --razor --mapmods --tag $decoyPrefix --pepxml ./interact.pep.xml --protxml ./interact.prot.xml # Open search

# Perform quantification.
$philosopherPath freequant --dir $dataDirPath

# Make reports.
$philosopherPath report
$philosopherPath workspace --clean

```
