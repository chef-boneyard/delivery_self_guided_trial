# Delivery Self Guided Trial
Welcome to the Delivery Self Guided Trial

Delivery Trials are invite only and require a license key to complete the install, so if you stumble here on your own please request an [INVITE](https://www.chef.io/delivery/).

These docs will guide you through setting up delivery and configuring pipelines once it is setup. You will install the delivery cluster on your own infrastructure using chef provisioning and your license key. We currently support two install methods. The first is AWS. Using this method provisioning will take care of creating all the resources and setting them up. The second is SHH. This method is used in all other environments and assumes you have created machines and have ssh access with passwordless SUDO on the boxes.

An important consideration in picking your install method/location is network access. If you will be integrating with any apis make sure you can access them from the environment you choose to install delivery in. Often times we setup a cluster only to find an internal api we want hit is not available. Think things like Jenkins or your own internal deployment tool, etc.

## Installation
1. Create a provisioning node:
  * [Creating a provisioning node](provisioning_node.md)
2. Setup to run provisioning:
  * [AWS Setup](aws.md)
  * [SSH Setup](ssh.md)
3. Run provisioning (from inside delivery-cluster):

        CHEF_ENV=delivery-cluster chef exec rake setup:cluster

    * Note: delivery-cluster should match the name of the environment file you created earlier.
    * Note: Sometimes the first converge fails on the build nodes run the above step again and it should fix it.
    * Note: For AWS this step creates instances. If there are any failures check your aws console for nodes without names. These can be removed.

4. Sanity Check (from inside delivery-cluster)
  * Chef Server
    1. Get Chef Server url

        ```cat ~/delivery-cluster/.chef/delivery-cluster-data/knife.rb```

    2. Navigate to 'chef_server_url' and login with 'delivery:delivery'
    3. Click on 'Nodes' you should see at least 4
  * Delivery
    1. Get Credentials and URL:

        ```cat ~/delivery-cluster/.chef/delivery-cluster-data/aws-example.creds```

      * aws-example should match your cluster id in the environment file.
    2. Navigate to the 'Web Login' and use the admin credentials to login
  * Build Nodes
    1. ```knife node status```
      * All build nodes should report available.
