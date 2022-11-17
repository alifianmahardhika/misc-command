## Installation of openmx (Linux)
### Preparation
1. Update and upgrade apt
```bash
sudo apt update && sudo apt upgrade
```
2. Install necessary package
```bash
sudo apt install make gcc g++ libnss3 gnuplot gnuplot-x11 emacs vim
```
3. Download Intel One API Toolkit [here](https://registrationcenter-download.intel.com/akdlm/irc_nas/17977/l_BaseKit_p_2021.3.0.3219_offline.sh)
4. Go into downloaded Intel One API Toolkit file location and install the toolkit
```bash
sudo bash l_BaseKit_p_2021.3.0.3219_offline.sh
```
5. Download Intel One API HPC Toolkit [here](https://registrationcenter-download.intel.com/akdlm/irc_nas/17912/l_HPCKit_p_2021.3.0.3230_offline.sh)
6. Go into downloaded Intel One API HPC Toolkit file location and install the toolkit
```bash
sudo bash l_HPCKit_p_2021.3.0.3230_offline.sh
```
7. After Installation of Intel One API and HPC Toolkit execute following command
```bash
source /opt/intel/oneapi/setvars.sh
```
8. Using an editor, add the following to the last line of the .bashrc
```
source /opt/intel/oneapi/setvars.sh
```
9. execute the following commands. If the version information is displayed, the installation has been successful.
```
icc --version
ifort --version
mpitun --version
```
