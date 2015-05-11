# SSH Install Guide

This guide will help you setup a Delivery cluster using SSH. This will
invlove creating 6+ new machines depending on what options you choose
to enable.

## Create Provisioning Node

You will need a provising node to manage your cluster:
[Creating a Provisioning Node](provisioning_node.md)

## Create Additional Nodes

You will next create nodes for the delivery infrastructure. For the
minimal setup you will need 5 additional nodes. In AWS we use
c3.xlarge machines (8 CPU 2.5GHz, 7.5 GiB Mem, 2 x40 GiB Disk). You
can probably get away with something a little smaller as long as you
have multiple cores. For each of these machines ensure you can ssh and
SUDO without a password from the provisioning node.

## SSH Specific Setup on Provisioning Node

There are few extra steps to do on your provisioning node if you are
using ssh. Run these from your local machine and replace with the
values for your keys.

1. Upload your aws private key:

        scp -i ~/.ssh/jmorrow-aws.pem ~/.ssh/jmorrow-aws.pem ubuntu@10.194.25.100:/home/ubuntu/.ssh/jmorrow-aws.pem

## Additional SSH Setup

You will need to make sure the appropriate ports open in the network
layer. Please refer to the docs in
[delivery-cluster](https://github.com/opscode-cookbooks/delivery-cluster)
for the list of ports required.

## Configure Chef Provisioning

Now that you have a provisioning node with all of the prerequisites
setup. The next step is to create a configuration file to drive chef
provisioning. We use an environment file to do this.

1. Make sure you are in your delivery-cluster directory

        cd ~/delivery-cluster

2. Ensure you have an 'environments' folder

        mkdir environments

3. Edit your environment file
    * The README.md in
      [delivery-cluster](https://github.com/opscode-cookbooks/delivery-cluster)
      has documentation about all the options in this file. This
      example gives you the minimal cluster setup. Be sure to replace
      values with those appropriate for your setup.

        ```vi environments/delivery-cluster.json```

        ```
        {
          "name": "delivery-cluster",
          "description": "A Delivery Cluster",
          "json_class": "Chef::Environment",
          "chef_type": "environment",
          "override_attributes": {
            "delivery-cluster": {
              "id": "ssh-example",
              "driver": "ssh",
              "ssh": {
                "ssh_username": "ubuntu",
                "key_file": "~/.ssh/jmorrow-aws.pem"
              },
              "delivery": {
                "ip": "33.33.33.11",
                "enterprise": "ssh-example",
                "version": "latest",
                "license_file": "/home/ubuntu/delivery.license"
              },
              "chef-server": {
                 "ip": "33.33.33.10",
                 "organization": "ssh-example"
              },
              "builders": {
                "count": 3,
                "1": { "ip": "33.33.33.14" },
                "2": { "ip": "33.33.33.15" },
                "3": { "ip": "33.33.33.16" }
              }
            }
          }
        }
        ```

    * You can name your environment file whatever you want just take
      note of the name because we use it in later steps.

#### [Continue in README](README.md)
