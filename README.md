# Open Stack CLI in Docker

Best way to run the Openstack CLI is to run it inside a Docker container which eliminates amy dependency hell and polluting your own machine.

## Configuration

The easiest way to get the CLI configured is to set the environment variables using the OpenStack RC file. And, to keep the configuration flexible, we will mount the config RC file onto the docker container and then source it inside.

## Download the OpenStack RC file

Log in to the OpenStack dashboard, choose the project for which you want to download the OpenStack RC file, on the Project tab, open the Compute tab and click Access & Security.
On the API Access tab, click Download OpenStack RC File and save the file. The filename will be of the form PROJECT-openrc.sh where PROJECT is the name of the project for which you downloaded the file.
Create a 'config' folder and copy the 'PROJECT-openrc.sh' there. We will mount this config RC file when we run the container.
 
## Run the CLI

# get the openstack cli image
docker pull rupakg/openstack-cli

# run the docker container mounting the config file from the location $(pwd)/config
docker run -it -v $(pwd)/config:/config rupakg/openstack-cli /bin/bash

# source the config file and input your password
$ source /config/PROJECT-openrc.sh

# test the cli
$ openstack --version


