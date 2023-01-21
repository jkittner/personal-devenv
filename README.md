[![pre-commit.ci status](https://results.pre-commit.ci/badge/github/jkittner/personal-devenv/main.svg)](https://results.pre-commit.ci/latest/github/jkittner/personal-devenv/main)

# personal-devenv

1. create new virtual machine using VirtualBox
1. install ubuntu 22.04 (jammy)
1. follow setup instructions
1. open terminal (<kbd>Ctrl</kbd> + <kbd>Alt</kbd> + <kbd>T</kbd>) and run (enter `sudo` password if asked)
   ```bash
   sudo apt update
   sudo apt upgrade -y
   sudo apt install gcc make perl  -y --no-install-recommends
   ```
1. click `Devices` -> `insert guest additions`
1. click on CD-symbol
1. right click `autorun.sh` -> `Run as a Program`
1. enter `sudo` password in prompt
1. reboot the machine
1. click `Devices` -> `Shared Clipboard` select `bidirectional`
1. copy your ssh keys that you're using for GitHub over to `~/ssh`

   - If you don't have one:

     1. run the following commands on the new VM
        ```
        ssh-keygen -t ed25519 -C "your_email@example.com"
        ```
     1. hit enter to save it to the default filename
     1. enter a password - it is safer! (you won't see the password while typing)

   - If you have a key you want to reuse, copy these files (the contents) to the new machine
     - `~/.ssh/id_ed25519` (private key)
     - `~/.ssh/id_ed25519.pub` (public key)
   - make sure `id_ed25519` and `id_ed25519.pub` are present

1. install git
   ```bash
   sudo apt install git --no-install-recommends -y
   ```
1. clone the repository where the Ansible playbooks are to `/tmp`
   ```bash
   cd /tmp
   git clone git@github.com:jkittner/personal-devenv
   cd personal-devenv
   ```
   or via https
   ```bash
   cd /tmp
   git clone https://github.com/jkittner/personal-devenv
   cd personal-devenv
   ```
1. create a virtual environment in the cloned repo
   ```bash
   wget -q https://bootstrap.pypa.io/virtualenv.pyz
   python3 virtualenv.pyz venv
   . venv/bin/activate
   ```
1. install requirements for Ansible
   ```bash
   pip install -r requirements.txt
   ```
1. run ansible (enter the password you set when installing the OS)
   ```bash
   ansible-playbook playbooks/jammy.yaml -i hosts.yaml -K
   ```
1. restart the machine, so the `docker` group is recognized
