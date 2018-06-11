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

#2. sudo apt-get update error.
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
