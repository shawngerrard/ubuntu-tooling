# ubuntu-tooling
Set of scripts, configurations, and instructions for reproducing my application tooling kit for the Ubuntu distribution of the Linux environment.

## Introduction

I use some standard tools for different things within each Linux environment. I've developed these instructions with 


### Update and Install Packages

First, let's ensure that the Apt package manager is up-to-date.

```sudo apt-get update && sudo apt-get upgrade```

Next, we will install a number of applications that would be used in a standard workflow or are a dependency for other tools.

```sudo apt-get install -y git locales curl wget xclip xsel tmux tmate net-tools less wget htop screenfetch zip openssh-client dictd knockd python3-pip emacs apt-transport-https software-properties-common ca-certificates dirmngr xterm xtermcontrol jq```

We'll use NodeJS package manager to install Bitwarden, but I've seperated this application from the above command in-case you use different secret managers.

```sudo apt-get install -y nodejs npm```

### Install Container Runtime (Docker)

I use Docker to run containers and create/test Docker images. 

Use the following code to add the Docker software repository to the Apt package manager, and then install Docker using Apt.

```
# Download and add Docker's official public PGP key.
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

# Add the `stable` channel's Docker upstream repository.
sudo add-apt-repository \
"deb [arch=amd64] https://download.docker.com/linux/ubuntu \
$(lsb_release -cs) \
stable"

# Update the apt package list and install docker packages.
sudo apt-get update -y && sudo apt-get install -y docker-ce docker-ce-cli containerd.io

# Allow your user to access the Docker CLI without needing root access.
sudo usermod -aG docker $USER

# Ensure the docker service is started
sudo service docker start
```

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


## Optional Packages

### Install Container Orchestrator (Kubernetes) - TO DO

I use Kubernetes to manage container and pod orchestration.

```
```

### Install Infrastructure Stack Manager (Pulumi) - TO DO

I use Pulumi to manage infrastructure stacks as code.

```
```
