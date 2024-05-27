# How to run the Rmd scripts?

<li>Go to <a href="https://console.cloud.google.com/compute/instances?hl=en&project=hotspotstoplight">GCP Virtual Machine console</a>. Connect to the 'landcoverchange' instance using ssh. </li>

<li> Start the docker env and then run it.</li>

```bash
sudo docker start r_env
sudo docker exec -it r_env sh
```

<li> Navigate to the LandCoverChange directory and pull the latests updates</li>

```bash
cd LandCoverChange
git pull
```

<li> Run the Rmd file</li>

```bash
Rscript -e "rmarkdown::render('lulcc_SanJose_cloud.Rmd')"
```

# How to update the dependencies of the docker container?

Read more [here]
Please refer to this [readme](./lulcc_VM_README.md) and this <a href="https://docs.google.com/document/d/1PCeHeQBrzPqB2EIIivNQSGX05viQ8mrJFdaSol5p1Pk/edit?pli=1#heading=h.m83mdxox0qq3">doc</a>.

# How to extend the memory of the VM instance?

<li>Go to <a href="https://console.cloud.google.com/compute/instances?hl=en&project=hotspotstoplight">GCP Virtual Machine console</a>. Click the 'landcoverchange' instance. </li>

<li> Click 'EDIT' on the top of the page. </li>

![alt text](/images/image.png)

<li> Scroll down, make sure the Machine type is 'CUSTOM' and 'Extend Memory' is enabled. You can adjust the memory here.  </li>

![alt text](/images/image-1.png)
