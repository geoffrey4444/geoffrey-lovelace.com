# The docker way

** Install docker **
https://www.docker.com/docker-mac

** Example docker commands **
*With a docker container named "python3"*
<code>
docker start python3 #start container
docker stop python3 #stop container
docker exec -it python3 /bin/bash -l #new shell in running container
docker ps -a #status of all containers
docker images #status of all images, including how much space they take up
</code>

** Docker reference **
<https://github.com/wsargent/docker-cheat-sheet>

# Terminal commands to make nice docker containers

** Generic jupyter/scipy/numpy/python3 **

<code>
docker pull jupyter/datascience-notebook
docker run -p 8892:8892 -v ${HOME}/.ssh:/home/jovyan/.ssh -v /Users/geoffrey/Dropbox\ \(Personal\)/:/home/jovyan/dropbox --name python3 -it jupyter/datascience-notebook /bin/bash -l
#In docker
jupyter notebook --ip 0.0.0.0 --port 8892 --no-browser
</code>

** pycbc **

<code>
docker run -p 8891:8891 -v ${HOME}/.ssh:/home/pycbc/.ssh -v /Users/geoffrey/Dropbox\ \(Personal\)/:/home/pycbc/dropbox --name pycbc_notebook -it pycbc/pycbc-el7:v1.8.2 /bin/bash -l
jupyter notebook --ip 0.0.0.0 --port 8891 --no-browser
</code>

** spectre **

<code>
mkdir $HOME/spectre
export SPECTRE_ROOT=$HOME/spectre
cd $SPECTRE_ROOT
git clone git@github.com:sxs-collaboration/spectre.git .
docker pull sxscollaboration/spectrebuildenv:latest
docker run -v ${SPECTRE_ROOT}:${SPECTRE_ROOT} --name spectre -i -t sxscollaboration/spectrebuildenv:latest /bin/bash
</code>

** spec **

<code>
mkdir $HOME/spec
export SPEC_ROOT=$HOME/spec
cd $SPEC_ROOT
git clone git@github.com:sxs-collaboration/spec.git .
docker pull sxscollaboration/specbuildenv
docker run -ti --name spec -v ${SPEC_ROOT:/home/specuser/spec sxscollaboration/specbuildenv
</code>

** Thermal noise code (uses dealii) **

<code>
docker pull dealii/dealii:v8.5.1-gcc-mpi-fulldepscandi-debugrelease mkdir ${HOME}/dealii
export DEALIIHOME=${HOME}/dealii
cd ${DEALIIHOME}
git clone git@git.ligo.org:geoffrey-lovelace/NumericalCoatingThermalNoise.git
docker run -ti --name dealii -v ${DEALIIHOME}:${DEALIIHOME} dealii/dealii:v8.5.1-gcc-mpi-fulldepscandi-debugrelease
</code>

** cleanup: docker can eat your disk space **

<code>
docker ps -a
docker rm CONTAINER #remove container
docker images
docker rmi IMAGE #remove image IMAGE
</code>

** Binder: **

Point to a github repo, and they make the notebooks in there available to everyone. Don't put in anything that uses lots of CPU power...run those locally or on a cluster

