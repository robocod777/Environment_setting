OS: Windows10 home

# 1.Install docker toolbox
(https://docs.docker.com/toolbox/toolbox_install_windows/)

## **CAUTION** When you install the docker toolbox, check "Install virtualbox"

Run Docker Quickstart Terminal

# 2. Make shared directory
## at VirtualBox, 
Setting->Shared Directory, add perminant shared directory named as "source" with path(e.g.c:\workspace\dockerws)

## at boot2docker
### Putty
enter the ip, and enter

> user: docker, pw: tcuser


```bsh
sudo vi /var/lib/boot2docker/bootlocal.sh
```
then,
```bsh
#!/bin/sh

mkdir -p /home/docker/source
mount -t vboxsf source /home/docker/source
```

Reboot then restart putty.
```bsh
sudo reboot -f
```

You can verify shared directory
```bsh
dk -k
```

# Pull and Run anaconda docker container
To use anaconda3,
(https://hub.docker.com/r/continuumio/anaconda3/)

- FYI Anaconda & Docker
(https://www.anaconda.com/blog/developer-blog/anaconda-and-docker-better-together-reproducible-data-science/)
Anaconda (https://conda.io/docs/user-guide/install/windows.html)

```bsh
docker pull continuumio/anaconda3
docker run -i -t continuumio/anaconda3 /bin/bash
```

Alternatively, you can start a Jupyter Notebook server and interact with Anaconda via your browser:
```bsh
docker run -i -t -p 8888:8888 continuumio/anaconda3 /bin/bash -c "/opt/conda/bin/conda install jupyter -y --quiet && mkdir /opt/notebooks && /opt/conda/bin/jupyter notebook --notebook-dir=/opt/notebooks --ip='*' --port=8888 --no-browser"
```
You can then view the Jupyter Notebook by opening http://localhost:8888 in your browser,  
or http://<DOCKER-MACHINE-IP>:8888 if you are using a Docker Machine VM.

# Conda Navigator
## opencv3 env
Create environment named "opencv3".  
Then, install package opencv=3.2.0 via conda.
```bsh
conda install -c conda-forge opencv=3.2.0
```
cf> I failed with "conda install opencv3"  

*** List of installed library ***
```
ca-certificates 2018.4.16
libwebp 0.5.2
certifi 2018.4.16
libtiff 4.0.9
jpeg 9b
numpy 1.13.3
opencv 3.2.0
openssl 1.0.2o
zlib 1.2.11
icu 58.2
mkl 2018.0.2
mkl fft 1.0.2
intel-openmp 2018.0.0
mkl_random 1.0.1
qt 5.6.2
libpng 1.6.34 
```

(optional) upgrade pip
```bsh
python -m pip install --upgrade pip
```
Run jupyter notebook
```bsh
jupyter notebook
```


## opencv env
create new environment as "opencv"  
Upgrade pip
```bsh
python -m pip install --upgrade pip
```

Download "up-to-date" opencv at (https://www.lfd.uci.edu/~gohlke/pythonlibs/#opencv)  
-> I failed with cp37. So I downloaded opencv_python‑3.4.1‑cp36‑cp36m‑win_amd64.whl
Change directory, and then install using wheel
```bsh
cd C:\(...)\Downloads
pip install opencv_python‑3.X.X‑cp36‑cp36m‑win_amd64.whl

```

Install numpy, matplotlib.   
NumPy and matplotlib are necessary to import cv2.
```bsh
pip install numpy
pip install matplotlib
```

```bsh
python
```
Import opencv library and look up the version of opencv quickly.

```python
import cv2
print(cv2.__version__)
3.4.1
```

Helpful Link: [Stack flow](https://stackoverflow.com/questions/42994813/installing-opencv-on-windows-10-with-python-3-6-and-anaconda-3-6)

# Set Jupyter Notebook Kernel with ipykernel

[Helpful link(Same problem: Import on Jupyter notebook failed where command prompt works.)](https://github.com/jupyter/notebook/issues/1524)  
In my case: cv2.

What I did:
```bsh
(openCV) HOME> AppData\Local\conda\conda\envs\openCV\python.exe -m pip install ipykernel
  Something installed.......
(openCV) HOME> AppData\Local\conda\conda\envs\openCV\python.exe -m ipykernel install
  Installed kernelspec python3 in C:\ProgramData\jupyter\kernels\python3
(openCV) HOME> AppData\Local\conda\conda\envs\openCV\python.exe -m ipykernel install --name Python3
  Installed kernelspec Python3 in C:\ProgramData\jupyter\kernels\python3
(openCV) HOME> AppData\Local\conda\conda\envs\openCV\python.exe -m ipykernel install --name PythonCV
  Installed kernelspec PythonCV in C:\ProgramData\jupyter\kernels\pythoncv
```

Then, launch jupyter notebook
```bsh
(oepnCV) HOME> jupyther notebook
```
I could find "PythonCV" kernel.
Make a new file with PythonCV, then 
```python
import cv2
print(cv2.__version__)
```
It works!

# Install "Pillow" to read 'jpg' images.
Error Msg I got:
```python
ValueError: Only know how to handle extensions: ['png']; with Pillow installed matplotlib can handle more images
```

Reason:  
"imread" can only read png images.

What I did:
```bsh
(openCV) HOME> cd AppData\Local\conda\conda\envs\openCV
(openCV) openCV> python.exe -m pip install pillow
```

[Reference](https://github.com/udacity/sdc-issue-reports/issues/69)

# Install "PyTorch" in OpenCV kernel.
First of all, I've added "conda" Path to the Environment variables.
'''C:\Users\joony\Anaconda3\Scripts\'''

Reference:  
[PyTorch(official?)](https://pytorch.org/#pip-install-pytorch)

My options: windows, conda, python3.6, None CUDA.  
**PyTorch**
```bsh
(openCV) conda.exe install pytorch-cpu -c pytorch
```
I used "conda.exe" instead of "conda".  
**torchvision**
```bsh
(openCV) HOME> cd AppData\Local\conda\conda\envs\openCV
(openCV) openCV> python.exe -m pip install cython
(openCV) openCV> python.exe -m pip install torchvision
```
Before installing torchvision, I have installed cython because error message below was appeared.
```
mkl-random 1.0.1 requires cython, which is not installed.
mkl-fft 1.0.0 requires cython, which is not installed.
```

# Add some libraries on OpenCV kernel.
**pandas**
```bash
(openCV) HOME> cd AppData\Local\conda\conda\envs\openCV
(openCV) openCV> python.exe -m pip install pandas
Installing collected packages: pandas
Successfully installed pandas-0.22.0
```

**scipy**
 ```bash
(openCV) HOME> cd AppData\Local\conda\conda\envs\openCV
(openCV) openCV> python.exe -m pip install scipy
Installing collected packages: scipy
Successfully installed scipy-1.1.0
```
