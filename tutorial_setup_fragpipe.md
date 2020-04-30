
## Setting up FragPipe

<br>
#### Install or update Java
FragPipe and MSFragger both require a 64-bit Java to run. Download 64-bit Java [here](https://www.java.com/en/download/manual.jsp) by selecting the Windows Offline 64-bit version. Launch the installer and follow the prompts. (You may need to restart FragPipe after updating Java.)  
<img src="https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/java_version_selection.png" width="700px" align="middle"/>


<br>
#### Install or update FragPipe
FragPipe can be downloaded [here](https://github.com/Nesvilab/FragPipe/releases). Follow the instructions on that same Releases page to launch the program.  When FragPipe launches, the first tab in the window ('Config') will be used to configure the program.


<br>
#### Install, update, or use an already downloaded version of MSFragger
**Use an existing MSFragger .jar file:** In FragPipe, use the 'Browse' button to select the .jar file.

**Update MSFragger:** In FragPipe, use the 'Update' button to upgrade to the latest version of the MSFragger .jar file. Click 'Choose file' to select your current .jar file, and select the latest release (we recommend downloading the zip version, as it can read raw LC-MS files).

**Download MSFragger for the first time:**
1. In FragPipe, select the 'Download' button to navigate to the download page. On the download page, click the 'BUY' button (cost: $0) to choose the offering appropriate for you (academic users should select the second option, all others should select the first).
2. Fill in your name and email, then review and accept the license terms. Provide the remaining information, and confirm. The bottom of the next page will have a link to download the first MSFragger release. Unzip this compressed file.
3. Use the 'Update' button in FragPipe to upgrade this first release to the latest version. Click 'Choose file' to select the .jar file you just downloaded, and select the latest release. **The zip version is strongly recommended, as it can read raw LC-MS files. Always keep the original directory structure of the MSFragger download (e.g. do not move the .jar file separately).**
4. In FragPipe, click 'Browse' to select the updated .jar file.

<br>
#### Install, update, or use an already downloaded version of Philosopher
If you have already downloaded Philosopher, use the 'Browse' button in FragPipe to select the latest Philosopher executable file. To upgrade to the most recent release or to download for the first time, use the 'Download' button.

<br>
#### Optional: install, update, or use an already installed version of Python
Database splitting (to reduce the size of the in-memory fragment ion index-- helpful for workstations with limited memory or for complex searches) and/or spectral library generation will require Python 3 or above.

**If you already have Python 3 or above**, make sure the following packages are installed: `numpy`, `pandas`, `matplotlib`, `Cython`, and `msproteomicstools`. The `easypqp` package is also required to build spectral libraries from timsTOF data. In most cases, you can run `pip install [package name]` to install each.

**If Python 3 is not already installed**:
1. From the [Anaconda download site](https://www.anaconda.com/distribution/), click 'Download' and select the latest Python version (3.7 or higher) and launch the installer.

<img src="https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/anaconda_install.png" width="500px" align="middle"/>
2. Follow the prompts in the graphical installer. Note the install location that you choose and complete the installation. We do not recommend adding Anaconda to your PATH environment variable, but you can choose to register Anaconda as your default Python.
<img src="https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/anaconda_install_path.png" width="500px" align="middle"/>

3. From the start menu, search for "Anaconda Prompt" and launch it.
<img src="https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/anaconda_prompt_search.png" width="700px" align="middle"/>

4. In the Anaconda Prompt window that opens, type `pip install msproteomicstools` and hit enter to install the package required for spectral library generation.
<img src="https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/pip_install.png" width="700px" align="middle"/>
6.  In FragPipe, use the 'Browse' button to navigate to the installation location and select **python.exe**.
![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/fragpipe_python.png)

<br>
#### Next: see the [FragPipe usage tutorial](https://msfragger.nesvilab.org/tutorial_fragpipe.html).

