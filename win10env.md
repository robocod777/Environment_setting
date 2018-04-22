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

Helpful Link [Stack flow](https://stackoverflow.com/questions/42994813/installing-opencv-on-windows-10-with-python-3-6-and-anaconda-3-6)

