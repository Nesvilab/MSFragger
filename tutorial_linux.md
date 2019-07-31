# Running a FragPipe-equivalent workflow on Linux

Following is a shell script demo. Modifying it accordingly.

```shell
#!/bin/bash

set -xe

# Specify paths of tools and files. Change them accordingly.
dataDirPath="data/"
fastaPath="2019-02-27-td-UP000005640_9606_2019_01.fasta"
msfraggerPath="MSFragger-20190530.jar"
fraggerParamsPath="fragger.params"
philosopherPath="philosopher.1.1.2"
crystalcPath="Crystal-C.jar"
crystalcParameterPath="crystalc.pepXML.params"
decoyPrefix="rev_"

# Run MSFragger. Change the number behind -Xmx according to your computer's memory size.
java -Xmx64G -jar $msfraggerPath $fraggerParamsPath $dataDirPath/*.mzML

# Move pepXML files to current directory.
mv $dataDirPath/*.pepXML ./

# Move tsv files to current directory.
mv $dataDirPath/*.tsv ./ # Comment this line if localize_delta_mass = 0 in your fragger.params file.

# Run Crystal-C If it is an open search, run Crystal-C. Otherwise, don't run it by commenting the following for-loop
for myFile in ./*.pepXML
do
	java -Xmx64G -cp $crystalcPath Main $crystalcParameterPath $myFile
done

# Run PeptideProphet, ProteinProphet, and FDR filtering inside Philosopher
$philosopherPath workspace --clean
$philosopherPath workspace --init
$philosopherPath database --annotate $fastaPath --prefix $decoyPrefix

# Pick one from the following three commands and comment rest of two.
$philosopherPath peptideprophet --nonparam --expectscore --decoyprobs --ppm --accmass --decoy $decoyPrefix --database $fastaPath ./*.pepXML # For closed search
$philosopherPath peptideprophet --nonparam --expectscore --decoyprobs --masswidth 1000.0 --clevel -2 --decoy $decoyPrefix --combine --database $fastaPath ./*.pepXML # For open search
$philosopherPath peptideprophet --nonparam --expectscore --decoyprobs --ppm --accmass --nontt --decoy $decoyPrefix --combine --database $fastaPath ./*.pepXML # For non-specific closed search

$philosopherPath proteinprophet --maxppmdiff 2000000 ./*.pep.xml

# Pick one from the following two commands and comment the other one.
$philosopherPath filter --sequential --razor --mapmods --tag $decoyPrefix --pepxml ./ --protxml ./interact.prot.xml # closed or non-specific closed search
$philosopherPath filter --sequential --razor --mapmods --tag $decoyPrefix --pepxml ./interact.pep.xml --protxml ./interact.prot.xml # open search

$philosopherPath report
$philosopherPath workspace --clean

```
