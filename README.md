# LifeTracker (iteration 2)

## Overview
This is the second iteration of the LifeTracker application, used for
demonstration purposes for a talk on the virtues of virtualisation (like
containerisation).

This iteration shows how one could deploy the application should one make use of
[Ansible](https://www.ansible.com/) for deployment.

The build/test/run instructions are available in the repo for the first
iteration, available [here](https://github.com/thanethomson/lifetracker-iter1).

## Additional Requirements
In addition to the software mentioned in iteration 1, you will need:

* [Python 3](https://www.python.org/)
* [VirtualBox](https://www.virtualbox.org/)
* [Ubuntu Server ISO](https://www.ubuntu.com/server)

## Deployment
### Virtual Machines
Make sure you've got 2 clean [Ubuntu Server](https://www.ubuntu.com/server) VMs
available on your machine (one for the application, and the other for the
database). You must have SSH and `sudo` access to/on those machines in order to
execute the Ansible playbooks.

### Hosts
Secondly, you'll need to update the `hosts` file in your repo with the IP
addresses of your VMs on your local network (one of the drawbacks of this
approach, if you don't have some kind of automatic DNS configuration for your
VMs).

### Virtual Environment
The recommended approach to configure Ansible is in a virtual environment, so
you don't have conflicts with different versions of the package or other
dependencies on your system:

```bash
> cd /path/to/lifetracker-iter2/deploy

# create the virtual environment
> python3 -m venv venv

# activate the virtual environment
> source venv/bin/activate

# install Ansible
> pip install ansible
```

### Deploy
To deploy the database, simply do the following:

```bash
> cd /path/to/lifetracker-iter2/deploy

# make sure virtual env is active
> source venv/bin/activate

# deploy
> ansible-playbook -kK deploy-db.yml
```

To deploy the application, do the following:

```bash
> ansible-playbook -kV deploy-app.yml
```

