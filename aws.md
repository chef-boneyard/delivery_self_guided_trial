# AWS Install Guide
This guide will help you setup a Delivery cluster in AWS. This will invlove creating 6+ new machines depending on what options you choose to enable.

## Create Provisioning Node
You will need a provising node to manage your cluster: [Creating a Provisioning Node](provisioning_node.md)

## AWS Specific Setup on Provisioning Node
There are few extra steps to do on your provisioning node if you are using aws. Run these from your local machine and replace with the values for your keys.

1. Upload your aws private key:

        scp -i ~/.ssh/jmorrow-aws.pem ~/.ssh/jmorrow-aws.pem ubuntu@10.194.25.100:/home/ubuntu/.ssh/jmorrow-aws.pem
        
2. Upload your aws configuration

        scp -i ~/.ssh/jmorrow-aws.pem -r ~/.aws ubuntu@10.194.25.100:/home/ubuntu/.aws

## Additional AWS Setup
You will need to have an aws security group with appropriate ports open. Please refer to the docs in [delivery-cluster](https://github.com/opscode-cookbooks/delivery-cluster) for the list of ports required.

## Configure Chef Provisioning
Now that you have a provisioning node with all of the prerequisites setup. The next step is to create a configuration file to drive chef provisioning. We use an environment file to do this.

1. Make sure you are in your delivery-cluster directory

        cd ~/delivery-cluster

2. Ensure you have an 'environments' folder

        mkdir environments

3. Edit your environment file
    * README.md in [delivery-cluster](https://github.com/opscode-cookbooks/delivery-cluster) has documentation about all the options in this file. This example gives you the minimal cluster setup. Be sure to replace values with those appropriate for your setup. 

        ```vi environments/delivery-cluster.json```

        ```
        {
          "name": "delivery-cluster",
          "description": "A Delivery Cluster",
          "json_class": "Chef::Environment",
          "chef_type": "environment",
          "override_attributes": {
            "delivery-cluster": {
              "id": "aws-example",
              "driver": "aws",
              "aws": {
                "key_name": "jmorrow-aws",
                "ssh_username": "ubuntu",
                "image_id": "ami-3d50120d",
                "subnet_id": "subnet-19ac017c",
                "security_group_ids": "sg-cbacf8ae",
                "use_private_ip_for_ssh": true
              },
              "delivery": {
                "flavor": "c3.xlarge",
                "enterprise": "aws-example",
                "version": "latest",
                "license_file": "/home/ubuntu/delivery.license"
              },
              "chef-server": {
                "flavor": "c3.xlarge",
                "organization": "aws-example"
              },
              "builders": {
                "flavor": "c3.large",
                "count": 3
              }
            }
          }
        }
        ```

    * You can name your environment file whatever you want just take note of the name because we use it in later steps.

#### [Continue in README](README.md)
