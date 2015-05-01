# AWS Install Guide
This guide will help you setup a Delivery cluster in AWS. This will invlove creating 6+ new machines depending on what options you choose to enable.

## Create Provisioning Node
You will need a provising node to manage your cluster: [Creating a Provisioning Node](provisioning_node.md)

## Configure Chef Provisioning
Now that you have a provisioning node with all of the prerequisites setup. The next step is to create a configuration file to drive chef provisioning. We use an environment file to do this.

1. Make sure you are in your delivery-cluster directory

        pwd

2. Ensure you have an 'environments' folder

        mkdir environments

3. Edit your environemnt file

        vi environments/delivery-cluster.json

        {
          
        }

    * You can name your environment file whatever you want just take note of the name because we use it in later steps.
