# Recruitment Task
All files used for development can be found in 'rectuitment-2024' directory.
# Docker
1. On a system with docker installed, start the app by running 'docker-compose up' in the main project directory (recruitment-2024) 
2. The output of the app can be observed on http://localhost:8000
3. Live Reloading is enabled - any changes made in the projects file structure or the code will be reflected immediately.
-------------------------------------------------------
# Cloud Hosting
I chose to host my app in Microsoft Azure. There I set up a virtual machine to host the contenerized application prepared in the first section.
1. Connect to the Ubuntu VM with ssh eficode@20.215.40.23. The provided public key was added and admin rights were granted to user eficode.
2. The project can be found in jakubogo user directory; there run 'docker-compose up' to get the app and proxy up and running.
3. The app can be accessed at http://20.215.40.23:8000/. The reverse proxy set on http://20.215.40.23/weatherapp is only able to communicate with the frontend portion of the application. I unfortunately wasn't able to solve this issue.
-------------------------------------------------------
# Terraform & Ansible
I used the VM from the previous section "weatherapp (20.215.40.23)" as an Ansible control-node and Terraform host. 
1. Connect to the control-node using ssh eficode@20.215.40.23. 
2. In order to spin up a new VM and deploy the weatherapp on it, run 'bash create-vm-deploy-weatherapp.sh' in 'jakubogo' directory. This script will spin up a new linux virtual machine using Terraform, install docker, docker-compose and deploy the weatherapp with Ansible. The app can then be viewed on 20.215.246.110:8000. Note, that to run this script, you have to be logged in to the Microsoft account, so I don't suppose you will be able to do it yourself, but it was tested and it works :).
3. The app can be torn down by running '/ansible/ansible-playbook compose-down.yml'.
4. Now the disappointing part - I wasn't able to dynamically change the ENDPOINT environment variable in the 'docker-compose.yaml' file. This means, that the app spun up using this script, will only work if the first instance on the control node is active. I am aware this is a no-go and defeats the entire purpose of this project, but I couldn't find a way to fix it - I would love to know the correct way to go about this, so I'll appreciate your feedback.
-------------------------------------------------------
# Summary and TODO
I am aware that my project has glaring shortcomings, most important one I mentioned in point 4. of the previous section. Anyhow, I had lots of fun working on this project. It was very interesting, I learned a lot and I'd love to know what it the state of the art approach to solving this issue. Regarding TODOs, I would surely want to automate the creation of the contol-node environment.
-------------------------------------------------------
# Weatherapp

There was a beautiful idea of building an app that would show the upcoming weather. The developers wrote a nice backend and a frontend following the latest principles and - to be honest - bells and whistles. However, the developers did not remember to add any information about the infrastructure or even setup instructions in the source code.
Luckily we now have [docker compose](https://docs.docker.com/compose/) saving us from installing the tools on our computer, and making sure the app looks (and is) the same in development and in production. All we need is someone to add the few missing files!

The idea of the exercise is to improve the bare-bone piece of code (i.e. the weatherapp) and ensure there's adequate infrastructure around it. 
In real life scenario we might suggest to our customers to leverage cloud services to just run code in a serverless fashion - but that would make it difficult to evaluate technical skills - and that's the whole point of this exercise, ain't it? 


## Returning your solution via Github
Use Github to work on the solution and hand it in. Don't forget to update the README file to make it clear what did you concentrate on.

* Make a copy of this repository in your own Github account (do not fork unless you really want to be public).
* Create a personal repository in Github.
* Make changes, commit them, and push them in your own repository.
* Send us the url where to find the code.

## Exercises

Here are some suggestions in different categories that you can do to make the app better. Before starting you need to get yourself an API key to make queries in the [openweathermap](http://openweathermap.org/). You can run the app locally using `npm i && npm start`.
Remember, this is not a test for a developer position, so we're not after extensive changes in javascript code. Rather, we'd like to see you be able to work comfortably with containers, VMs in cloud and ideally, Ansible.

### Docker

* Add **Dockerfile**'s in the *frontend* and the *backend* directories to run them virtually on any environment having [docker](https://www.docker.com/) installed. It should work by saying e.g. `docker build -t weatherapp_backend . && docker run --rm -i -p 9000:9000 --name weatherapp_backend -t weatherapp_backend`. If it doesn't, remember to check your api key first.

* Add a **docker-compose.yml** -file connecting the frontend and the backend, enabling running the app in a connected set of containers.

* The developers are still keen to run the app and its pipeline on their own computers. Share the development files for the container by using volumes, and make sure the containers are started with a command enabling hot reload.

### Cloud hosting

* Set up the weather service in a free cloud hosting service, e.g. [Azure](https://azure.microsoft.com/en-us/free/), [AWS](https://aws.amazon.com/free/) or [Google Cloud](https://cloud.google.com/free/).
* Enable external access to weather app via HTTP reverse proxy. We suggest creating one compute instance e.g. for AWS one EC2 instance, that will host both weather app and before mentioned proxy. Remember that Weather App should be exposed in a secure way.
* Enable external SSH access and add id_rsa_internship.pub key, which you can find in this repository. We would like to check your work so grant us admin rights on your test system.

### Ansible

* Write [Ansible](http://docs.ansible.com/ansible/intro.html) playbooks for installing [docker](https://www.docker.com/) and the app itself. These playbooks should work both for local and cloud environment.

#### Terraform

* Write [Terraform](https://www.terraform.io/) configuration files to set up infrastructure required to run the app in the cloud provider of your choice.

### Documentation

* Remember to update the README

* Use descriptive names and add comments in the code when necessary

### ProTips

* The app must be ready to deploy and work flawlessly.

* Detailed instructions to run the app should be included in your forked version because a customer would expect detailed instructions also.

* Extra points for making sure the app could be deployed with as few manual steps as possible.

* Feel free to add would-be-nice-to-haves in the app / infra setup that you didn't have time to complete as possible further improvements in README.
