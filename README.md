# Jenkins-installation-Linux
This repository holds the steps I took in installing Jenkins on a Linux virtual machine. The installation instruction are valid for Ubuntu distributions; the version I used was Ubuntu 20.04.

**Step 1** - Install Jenkins by running the commands below:

```bash
wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > \
  /etc/apt/sources.list.d/jenkins.list'
sudo apt-get update
sudo apt-get install jenkins
```

This package installation will perform multiple actions. Not only it will setup Jenkins as a daemon launched on start, but it will create a Jenkins user to run this service. Furthermore, the console log will direct its output to the /var/log/jenkins/jenkins.log file, which is useful to check while troubleshooting. Next, the installation will make sure /etc/default/jenkins gets populated with configuration parameters for the program's launch (such as JENKINS_HOME). Then the last but not least, Jenkins will be set to function on port 8080, which must be accessed through the browser to start configuration.

**Step 2** - Install Java. Update the repositories by running:

```bash
sudo apt update
```

Check the available packages:

```bash
sudo apt search openjdk
```

Pick one of the previously returned packages and install it.

> Note: Java 8 and Java 11 are, at the time of writing, the only supported runtime environments.

```bash
sudo apt install openjdk-11-jdk
```

Check the installation.

```bash
java -version
```

**Step 3** - Set up Jenkins by accessing:

```bash
localhost:8080
```

A prompt will then pop up, asking for the admin password, which can be found by running:

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

The next step is to customise Jenkins either by manually installing plugins, or by allowing the system to automatically install the most used and up-to-date ones. I chose the later option. The last steps would be to create another admin user instead of keeping the initial one and to restart the system for the final configuration of the installed plugins.
