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

### Install Code Editor (Microsoft Visual Studio Code)

I use VSCode as my go-to integrated development environment.

Use the following code to add the VSCode software repository to the Apt package manager, and then install VSCode using Apt.

```
# Download and add Microsoft's official public PGP key
wget -q https://packages.microsoft.com/keys/microsoft.asc -O- | sudo apt-key add -

# Add the `stable` Microsoft upstream repository
sudo add-apt-repository "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main"

# Install VSCode from Apt
sudo apt-get install -y code
```

### Install Secrets Manager (Bitwarden)

```
# Install the bitwarden cli via node package manager
sudo npm install -g @bitwarden/cli

# Test login to bitwarden
bw login <sign-up email>
```

