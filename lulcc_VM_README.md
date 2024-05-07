# Here are the steps used to run our land cover change modeling script on a Virtual Machine:

## Pull the docker base image we need to our local machine
### Here we use the r-base, with base R environment installed
```bash
docker pull r-base
```

## Run the docker image
### Now we have the docker image locally, we can enter the environment using this line.
```bash
docker run -it [image-name] sh
```

##Next, we install additional dependencies in a container
```bash
apt-get update
apt-get upgrade
apt-get install git
git clone [github repo]

apt-get install pandoc
apt-get install aptitude
```


##Here, the ‘aptitude’ is a useful tool to solve dependency issues when installing a package. Whenever there are ‘unmet dependencies’ issues using apt-get, use ‘aptitude’ instead. There are some examples in the code below.

##An important step is to install the package ‘terra’, instructions are shown here https://github.com/rspatial/terra. But we will meet multiple bugs in our environment. Follow the following codes to install it. 
```bash
install.packages("Rcpp")

aptitude install software-properties-common
apt-get install python3-launchpadlib
apt install gpg-agent

add-apt-repository ppa:ubuntugis/ubuntugis-unstable
apt-get update
```

# you may encounter problems executing the following line
# use ‘aptitude install libgdal-dev’ instead, and remember to look at the given suggestions carefully in case that some of the required dependencies are deleted.
```bash
apt-get install libgdal-dev libgeos-dev libproj-dev 
```

# Now open R CLI (simply enter ‘R’ in the command line)
```bash
remotes::install_github("rspatial/terra")
install.packages('remotes')
install.packages("rmarkdown")
install.packages("lulcc")
install.packages("randomForest")
install.packages("gsubfn")
install.packages("caret")
```

## If everything goes right, we should be able to run our Rmarkdown code within the docker environment by navigating to the correct directory and executing the following line.
```bash
Rscript -e "rmarkdown::render('lulcc_SanJose.Rmd')"
```

## Build a New Image and Push it to Hub
### Exit the container and run the following code locally to push the image to Docker hub. Similar to git, we need to first commit and then push. 
```bash
docker commit [container id] [new image name]
```

## For example
```bash
docker commit jinze10 hotspotstoplight
```

## we need to tag it before push
```bash
docker tag hotspotstoplight [username]/hotspotstoplight 
docker login
docker push [username]/hotspotstoplight
```

## Now we can see our image on the docker hub.

## Now we can enter into the VM via SSH
### If you haven’t done so already, pull the image to the VM
```bash
sudo docker pull jinze10/hotspotstoplight
```

## List all the containers in the VM
```bash
sudo docker ps
```

## You should be able to find a container called ‘r_env’.
### Start it and then run it.
```bash
sudo docker start r_env
sudo docker exec -it r_env sh
```

# Great! Now you have entered the docker container on a VM.

## Navigate to the LandCoverChange directory:
```bash
cd LandCoverChange
```
## pull the code from github:
```bash
git pull
```
## Now we can finally run the Rmd file
```bash
Rscript -e "rmarkdown::render('lulcc_SanJose_cloud.Rmd')"
```
