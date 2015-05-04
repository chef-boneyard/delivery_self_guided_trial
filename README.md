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

4. [Sanity Check](sanity_check.md) (from inside delivery-cluster)
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

## Setup Delivery
In delivery there are multiple levels of organization they are enterprises, organizations, and projects. The provisioning step created the initial enterprise you specified in your environment file. Enterprises are designed to be units of multi-tenency with separate sets of organizations and users. Next we will setup the delivery by adding users and organizations.

### Create an organization
We normally suggest creating a sandbox org where you can have a test project to play around with.

1. Log into the webui with the admin credentials you got earlier

        cat ~/delivery-cluster/.chef/delivery-cluster-data/aws-example.creds
       
2. Click 'Organizations' in the left column
3. Click the large orange box on left in header
4. Enter organization name (sandbox) and save

### Create users
If you set this up ldap integration you still need to create users in delivery, but we will use ldap to get most of the user details and to authenticate them.

1. Log into the webui with the admin credentials you got earlier

        cat ~/delivery-cluster/.chef/delivery-cluster-data/aws-example.creds
       
2. Click 'Users' in the left column
3. Click the large grey box on left in header
4. Enter user details and save (Give yourself all roles)
5. Sign-out of the 'admin' acocunt by clicking the user block in the left column (top dark blue box)
6. Sign-in with your account
7. Create any additional users you need

## Setup workstation

1. Install build-essential on linux or developer tools on mac
2. [Install Git](http://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
3. [Install Chefdk](https://downloads.chef.io/chef-dk/)
4. Install 'knife push': ```chef gem install knife-push```
5. [Install Delivery CLI](install_cli.md)

## Creating Projects, Pipelines, and Changes
We will work through a few examples to give you a sense of the different paths to get a project going in Delivery:

1. [Create and Import a new cookbook](new_cookbook.md)
2. [Import and existing cookbook](import_cookbook.md)
3. [Create cookbook manual delivery steps](new_cookbook_manual.md)

## LICENSE AND AUTHORS
- Author: Jon Morrow (<jmorrow@chef.io>)

```text
Copyright:: 2015 Chef Software, Inc

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```
