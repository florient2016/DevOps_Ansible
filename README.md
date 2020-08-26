# Devop_Ansible
install and configure docker using ansible playbook
## Automate Docker with Ansible 
Ansible is the way to automate Docker in your environment. Ansible enables you to operationalize 
your Docker container build and deployment process in ways that you’re likely doing manually today, or not doing at all.
## Operation system 
```
Red Hat Enterprise Linux 8.1
Centos 8
debian
```
## Install docker repolist using ansible playbook
Before install docker you need to setup docker repolist
### In debian distribution, installation will be made by "apt-get"
Install using the repository
```
sudo apt-get update
```
Add Docker’s official GPG key:
```
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
````
Install docker 
```
$ sudo apt-get update  $$ apt-get install docker-ce docker-ce-cli containerd.io
```
### Installation on redhat using ansible playbook
create a repolist file on /etc/yum.repo.d/
 ```
 name: Create docker repolist
  file:
    path: /etc/yum.repos.d/dockerFile.repo
    state: touch
    ignore_errors: yes
 ```
 Download an install docker repolist on docker official web site
 ```
 - name: add docker repolist
      get_url:
        url: https://download.docker.com/linux/centos/docker-ce.repo
        dest: /etc/yum.repos.d/docker.repo
```
### prerequis before install docker
on the remote make sure you install 
- containerd 
There are many different ways to use containerd:
If you are a developer working on containerd you can use the ctr tool to quickly test features and functionality without writing extra code
If you want to integrate containerd into your project, you can use a simple client package. In this guide, w
e will pull and run a Redis server with containerd using that client package.
```
- name: install cointened - prerequis for docker installation
      package:
        name: containerd
        state: absent
- name:  install containerd
  package:
    name: https://download.docker.com/linux/centos/7/x86_64/stable/Packages/containerd.io-1.2.6-3.3.el7.x86_64.rpm
    state: present
 ```
 - install python 3 and docker sdk for python 
 ```
 - name: INstall python3 
 command:"yum install python3-pip -y"
 - name: docker sdk for python
 command: pip3 install docker
 ignore_errors: yes
 ```
### Install docker package
```
- name: install docker --nobest
      command: "yum install docker-ce -y --nobest"
```
### Start docker service
```
- name: Start docker service
  package:
    name: docker
    state: started
    enable: yes
```

 
 
