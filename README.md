# ubuntu-tooling
Set of scripts, configurations, and instructions for reproducing my application tooling kit for the Ubuntu distribution of the Linux environment.

## Introduction

I use some standard tools for different things within each Linux environment. I've developed these instructions with 

First, let's ensure that the Apt package manager is up-to-date.

```sudo apt-get update && sudo apt-get upgrade```

## Install General Tools

I primarily use the tools in this section generally, and make these my priority to install.

### Install Standard Packages

Let's install a number of applications that would be used in a standard workflow or are a dependency for other tools.

```sudo apt-get install -y git locales curl wget xclip xsel tmux tmate net-tools less wget htop screenfetch zip openssh-client dictd knockd python3-pip emacs apt-transport-https software-properties-common ca-certificates dirmngr xterm xtermcontrol jq```

We'll use NodeJS package manager to install Bitwarden - note that I've seperated this application from the above command in-case you use a different secrets manager.

```sudo apt-get install -y nodejs npm```

### Install Secrets Manager (Bitwarden)

I use BitWarden to manage my secrets and other things that I want to keep secured.

```
# Install the bitwarden cli via node package manager
sudo npm install -g @bitwarden/cli

# Test login to bitwarden
bw login <sign-up email>
```

### Install Telecommunications Platform (Discord)

I use Discord to interact through VOIP with my people. This application is heavy, but provides crisp, high-quality audio and video communication.

> **Note:** If you're looking for more secure, professional ways of communicating via VOIP, you may want to try these open-source alternatives to TeamSpeak: [Matrix](https://matrix.org/) or [Mumble](https://www.mumble.info/).

```
# Install using Snap
snap install discord
```

> **Note:** To remove Discord, use ```sudo snap remove discord```.

### Install Game Installer Client (Steam)

Last, but certainly not least, I use Steam to obtain and manage my gaming applications.

We'll need access to the *multiverse* apt repository to get Steam.

```
# Add the `multiverse` repository to the Apt package manager
sudo add-apt-repository multiverse

# Install Steam from Apt
sudo apt install steam
```

## Optional - Install Infrastructure Tools

### Install Container Runtime (Docker)

I use Docker to run containers and create/test Docker images. 

Use the following code to add the Docker software repository to the Apt package manager, and then install Docker using Apt.

```
# Navigate to the `Downloads` folder
cd ~/Downloads

# Download and add Docker's official public PGP key
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

# Add the `stable` channel's Docker upstream repository
sudo add-apt-repository \
"deb [arch=amd64] https://download.docker.com/linux/ubuntu \
$(lsb_release -cs) \
stable"

# Update the apt package list and install docker packages
sudo apt-get update -y && sudo apt-get install -y docker-ce docker-ce-cli containerd.io

# Allow your user to access the Docker CLI without needing root access
sudo usermod -aG docker $USER

# Ensure the docker service is started
sudo service docker start
```

### Install Container Orchestrator (Kubernetes)

I use Lightweight Kubernetes (K3S) to manage container and pod orchestration. 

I install K3S without Traefik, as I generally like to use Nginx in my setup.

```
# Navigate to the `Downloads` folder
cd ~/Downloads

# Download the K3S install script and run it
curl -sfL https://get.k3s.io | sh -s - server --write-kubeconfig-mode 644 --no-deploy traefik
```

### Install Kubernetes Package Manager (Helm)

```
# Navigate to the `Downloads` folder
cd ~/Downloads

# Download the Helm install script
curl -sfSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3

# Update permissions to access the script
chmod 700 get_helm.sh

# Run the Helm install script
sudo ./get_helm.sh
```

### Install Infrastructure Stack Manager (Pulumi)

I use Pulumi to manage infrastructure stacks as code.

```
# Navigate to the `Downloads` folder
cd ~/Downloads

# Download the Pulumi install script and run it
curl -fsSL https://get.pulumi.com | sh
```

To bring up the Asterion infrastructure, we will need to clone the Git repository and configure our Pulumi setup.

```
# Navigate to the `Documents` folder
cd ~/Documents

# Obtain the Asterion infrastructure
git clone git@github.com:<username>/asterion-as-code

# Initialize the Pulumi stack
cd asterion-as-code && pulumi stack init

# Select the Pulumi stack
pulumi stack select asterion-as-code

# Initialize a Python virtual environment
python3 -m venv venv

# Activate the environment
source venv/bin/activate

# Install Pulumi project dependencies
pip install -r requirements.txt

# Start the Pulumi stack
pulumi up -y
```