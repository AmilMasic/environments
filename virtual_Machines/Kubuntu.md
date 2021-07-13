## Kubuntu Setup

- Download img from [Kubuntu.org](https://kubuntu.org/)
- Set up env on VM for 8 GB RAM.
- Set up 30 GB of hard disk space
- Follow installation menu, easy to execute
- no need for partitions, Kubuntu does it on its own.
- Once installed, update all the apps
- This might take some time

### Chrome and nodejs

- easiest way to install chrome is via the command line, atleast for me. Run `wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb`, followed by `sudo apt install ./google-chrome-stable_current_amd64.deb`
- run `sudo apt-get -y install curl postgresql libpq-dev default-jre build-essential phantomjs`
this will install all the products listed at the same time.
- run `curl -sL https://deb.nodesource.com/setup_11.x | sudo -E bash -
`
- if you get an error saying `curl not found` run `sudo apt-get install curl`
- since this means the previous command didn't run properly best to separate it into independent lines
- run `sudo apt-get install postgresql`, yes to install it
- run `sudo apt-get install libpq-dev`,
- `sudo apt-get install default-jre`
- `sudo apt-get install build-essential`
- phantomjs is going to follow a different approach
- original guide line found on [Gist site](https://gist.github.com/julionc/7476620)
- copied the information here just in case in gets deleted. [file](https://github.com/AmilMasic/environments/blob/master/virtual_Machines/installPhantomJsOnUbuntu.md)
- once phantomjs is operating, run `sudo apt-get install nodejs`
-

### vim, ack-grep and yarn
- run `sudo apt-get install ack-grep`
ack-grep is an advanced search tool in the terminal
- run `sudo apt-get install vim` to install vim editor
- run `sudo apt-get install nano` as an alternative to vim, it might already be installed
- yarn always is trouble, if the default `npm install -g yarn` fails, run `curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -` followed by `echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list`
afterwhich run `sudo apt update && sudo apt install yarn`

### file permision
- run these commands:
`sudo chown root:staff /usr/bin
sudo chmod 0775 /usr/bin
sudo chown -R root:npm /usr/lib/node_modules
sudo chmod 0775 /usr/lib/node_modules`
to allow file permisions to allow usage of some files

### setting up rbenv and rails

- follow guide on the [file](https://github.com/AmilMasic/environments/blob/master/virtual_Machines/rbenvGuide.md) or checkout the [original post](https://gorails.com/setup/ubuntu/21.04)
- after the guide, install some gems
- `gem update --system`
- `gem install phantomjs`
- `gem install pg`
- `gem install sqlite3`
- `gem install rails -v 6.1.3.2` obviously update the version to the one you need to use.
- run `rbenv rehash` once rails is installed
- run `rails -v` to check on it and make sure everything is installed properly


### setting up GitHub
- we need to replace Name and email in the below guide with our information that we signed up for with GitHub.
- `git config --global color.ui true`
- `git config --global user.name "YOUR NAME"`
- `git config --global user.email "YOUR@EMAIL.com"`
- `ssh-keygen -t rsa -b 4096 -C "YOUR@EMAIL.com"`
- the last command should give a prompt, type out yes and click enter on creating a password.
- to access the key type `cat ~/.ssh/id_rsa.pub`
- now copy the entire message and visit [SSH site on github](https://github.com/settings/keys)
- on this site click on add new ssh key and paste the information in.
- you can check your work by typing `ssh -T git@github.com`
- if prompted, enter yes and the following message should look like "Hi excid3! You've successfully authenticated, but GitHub does not provide shell access."
