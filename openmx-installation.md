## Installation of OpenMX (Linux)
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

## Installing OpenMX
Do these steps only after confirming above preparation steps is completely finished.
1. Download OpenMX 3.9 [here](https://www.openmx-square.org/openmx3.9.tar.gz)
2. Download the latest patch [here](https://www.openmx-square.org/bugfixed/21Oct17/patch3.9.9.tar.gz)
3. Go to OpenMX source file location and execute following commands
```bash
tar xvf openmx3.9.tar.gz
cp ./patch3.9.9.tar.gz openmx3.9/source
cd openmx3.9/source
tar xvf patch3.9.9.tar.gz
mv kpoint.in ../work/
```
4.  In the openmx3.9/source makefile, specify the following using an editor
```
MKLROOT = /opt/intel/oneapi/mkl/2021.3.0/
CC = mpiicc -O3 -xHOST -ip -no-prec-div -qopenmp -I${MKLROOT}/include -I${MKLROOT}/include/fftw
FC = mpiifort -O3 -xHOST -ip -no-prec-div -qopenmp
LIB= -L${MKLROOT}/lib/intel64 -lmkl_scalapack_lp64 -lmkl_intel_lp64 -lmkl_intel_thread -lmkl_core -lifcore -lmkl_blacs_intelmpi_lp64 -liomp5 -lpthread -lm -ldl
```
5. After that install OpenMX using these command
```bash
make all && make install
```
If make process is failed, try to change the gcc compiler to use older version for example gcc-9 in this case try to execute following commands:
```bash
sudo apt install gcc-9 g++-9
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-9 50
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-9 50
echo 'export CXX=/usr/bin/gcc-9' >> ~/.bashrc
```
And then relaunch your terminal and try to make again.

6. When the installation is completed successfully, the executable file: openmx will be generated in "openmx3.9/work"
7. Test Run using following command inside **openmx3.9/work** folder location
```bash
mpirun -np 4 ./openmx -runtest -nt 1
```
