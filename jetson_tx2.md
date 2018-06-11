OS: Ubuntu16.04 aarch64

# 1. Jetpack Install (Update?)
Jetpack download 3.2/
## Memo
I tried installing with "sudo apt -f install" without any package name several times.
I couldn't install at once.

After installing, 
```bsh
$ cd NVIDIA_CUDA-9.0_Samples/bin/aarch64/linux/release
$ ./oceanFFT
```

#2. sudo apt-get update

## Keyserver Problem.
```bsh
W: GPG error: file:/var/cuda-repo-9-0-local  Release: The following signatures couldn't be verified because the public key is not available: NO_PUBKEY XXXXXXXXXXXXXXXX
W: The repository 'file:/var/cuda-repo-9-0-local  Release' is not signed.
N: Data from such a repository can't be authenticated and is therefore potentially dangerous to use.
N: See apt-secure(8) manpage for repository creation and user configuration details.
W: GPG error: file:/var/nv-tensorrt-repo-ga-cuda9.0-trt3.0.4-20180208  Release: The following signatures couldn't be verified because the public key is not available: NO_PUBKEY XXXXXXXXXXXXXXXX
W: The repository 'file:/var/nv-tensorrt-repo-ga-cuda9.0-trt3.0.4-20180208  Release' is not signed.
N: Data from such a repository can't be authenticated and is therefore potentially dangerous to use.
N: See apt-secure(8) manpage for repository creation and user configuration details.
```
Solution: Add a public key. [link](https://devtalk.nvidia.com/default/topic/1030831/jetpack-3-2-mdash-l4t-r28-2-production-release-for-jetson-tx1-tx2/?offset=14#5245450)
```bsh
$ sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys XXXXXXXXXXXXXXXX
```
## lock Problem
```bsh
E: Could not get lock /var/lib/dpkg/lock - open (11: Resource temporarily unavailable)
E: Unable to lock the administration directory (/var/lib/dpkg/), is another process using it?
```
Solution: kill the process that uses apt. [link](https://askubuntu.com/questions/15433/unable-to-lock-the-administration-directory-var-lib-dpkg-is-another-process)
```bsh
$ ps aux | grep apt
$ kill process#
```


# 3. Packages


## pip
```bsh
$ sudo apt-get install python3-pip
$ pip3 install --upgrade setuptools
$ pip3 install --upgrade pip
```
Additional Packages:
```bsh
The following additional packages will be installed:
  libexpat1-dev libpython3-dev libpython3.5-dev python-pip-whl python3-dev
  python3-setuptools python3-wheel python3.5-dev
Suggested packages:
  python-setuptools-doc
The following NEW packages will be installed:
  libexpat1-dev libpython3-dev libpython3.5-dev python-pip-whl python3-dev
  python3-pip python3-setuptools python3-wheel python3.5-dev
0 upgraded, 9 newly installed, 0 to remove and 28 not upgraded.
```

After upgrade pip, I got a trouble.
```bsh
Traceback (most recent call last):
  File "/usr/bin/pip3", line 9, in <module>
    from pip import main
ImportError: cannot import name 'main'
```
Solution: Edit /use/bin/pip3 [link](https://github.com/pypa/pip/issues/5240#issuecomment-381662679)
```python
#I upgraded with pyenv, both python2 and python3, now pip2 not work and pip3 works
#After comparing pip2 and pip3, the difference is the import line

#pip2
from pip import main

#pip3
from pip._internal import main

After substitute pip2 import line with pip3 version, it works
```

## python3.6 and pip3 (python3.6)
```bsh
$ add-apt-repository ppa:jonathonf/python-3.6
$ sudo apt-get update
$ sudo apt-get install python3.6
$ sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.5 1
$ sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.6 2
$ sudo update-alternatives --config python3
```
then select '2'.

```bsh 
$ pip3 -V
pip 10.0.1 from /home/nvidia/.local/lib/python3.6/site-packages/pip (python 3.6)
```

## virtualenv
```bsh
$ pip3 install virtualenv. 
```
Add "/home/nvidia/.local/bin" to PATH@.bashrc.

```bsh
nvidia@tegra-ubuntu:~$ mkdir envCV
nvidia@tegra-ubuntu:~$ virtualenv --no-site-packages envCV
Using base prefix '/usr'
New python executable in /home/nvidia/envCV/bin/python3
Also creating executable in /home/nvidia/envCV/bin/python
Installing setuptools, pip, wheel...done.

nvidia@tegra-ubuntu:~$ source envCV/bin/activate
(envCV) nvidia@tegra-ubuntu:~$ 
```

```bsh
(envCV) nvidia@tegra-ubuntu:~$ python -V
Python 3.5.2
(envCV) nvidia@tegra-ubuntu:~$ deactivate
nvidia@tegra-ubuntu:~$ python -V
Python 2.7.12
nvidia@tegra-ubuntu:~$ 
```

