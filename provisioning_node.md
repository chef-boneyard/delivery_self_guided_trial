# Create Provisioning Node
We use chef-provisioning to create, upgrade, and manage the Delivery Cluster. While it can be done from a workstation, we generally suggest creating a provisioning node for this purpose. This allows you to have a central place from witch to manage the cluster and control who is allowed to manage it.

## Create Provisioning Node
Use your existing means to provision a new node with one of our supported platforms. This machine does not need to be very powerful since it just runs the provisioning code. In AWS we generally use an t2.micro (1 CPU 2.5GHz, 1 GiB Mem, 8 GiB Disk).

## Setup Provisioning Node
If you choose not to use a provisioning node do this on your workstation. These use generic install instructions for the prerequisites if you perfer a different install method it should be fine to use your own. You will want open these links in a new tab.

1. Install development environment
	* Debian based (apt)
        ```bash 
        apt-get install build-essential
        ```
    * RHEL based (yum)
        ```bash 
        yum groupinstall "Development Tools"
        ```
    * OS X
        ```bash 
        xcode-select --install
        ```

2. [Install Git](http://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
3. [Install Chefdk](https://downloads.chef.io/chef-dk/)
4. Install 'knife push': ```chef gem install knife-push```
5. Get License Key: ```curl -o delivery.license '{your_license_url}'```
6. Get Delivery Cluster: ```git clone https://github.com/opscode-cookbooks/delivery-cluster.git```

#### [Continue in README](README.md)
