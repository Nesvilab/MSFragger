## Setting up FragPipe

##### FragPipe can be downloaded [here](https://github.com/Nesvilab/FragPipe/releases). Follow the instructions on that same Releases page to launch the program.  When FragPipe launches, the first tab in the window ('Config') will be used to configure the program. A basic usage tutorial can be found [here (https://msfragger.nesvilab.org/tutorial_fragpipe.html).

#### Install, update, or use an already downloaded version of MSFragger
**Use an existing MSFragger .jar file:** Use the 'Browse' button to select the .jar file.

**Update MSFragger:** Use the 'Update' button to upgrade to the latest version of the MSFragger .jar file. Click 'Choose file' to select your current .jar file, and select the latest release (we strongly recommend downloading the zip version, as it can read raw LC-MS files).

**Download MSFragger for the first time:**
1. Select the 'Download' button to navigate to the download page. On the download page, click the 'BUY' button (cost: $0) to choose the offering appropriate for you (academic users should select the second option, all others should select the first).
2. Fill in your name and email, then review and accept the license terms. Provide the remaining information, and confirm. The bottom of the next page will have a link to download the first MSFragger release. Unzip this compressed file.
3. Use the 'Update' button in FragPipe to upgrade this first release to the latest version. Click 'Choose file' to select the .jar file you just downloaded, and select the latest release (the zip version is recommended, as it can read raw LC-MS files).
4. In FragPipe, click 'Browse' to select the updated .jar file.


#### Install, update, or use an already downloaded version of Philosopher
If you have already downloaded Philosopher, use the 'Browse' button to select the latest Philosopher executable file. To upgrade to the most recent release or to download for the first time, use the 'Download' button.


#### Optional: install, update, or use an already installed version of Python
Database splitting (to reduce the size of the in-memory fragment ion index-- helpful for workstations with limited memory or for complex searches) and/or spectral library generation will require Python 3 or above.

**If you already have Python 3 or above**, make sure the following packages are installed: `numpy`, `pandas`, `Cython`, and `msproteomicstools`.

**If Python 3 is not already installed**:
1. From the [Anaconda download site](https://www.anaconda.com/distribution/), select the latest Python version (3.7 or higher) and launch the installer.
![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/anaconda_install.png)

2. Follow the prompts in the graphical installer. Note the install location that you choose and complete the installation.
![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/anaconda_install_path.png)

3.  In FragPipe, use the 'Browse' button to navigate to the installation location and select **python.exe**.
![](https://raw.githubusercontent.com/Nesvilab/MSFragger/master/images/fragpipe_python.png)

<br>
#### Next: see the [FragPipe usage tutorial](https://msfragger.nesvilab.org/tutorial_fragpipe.html).

