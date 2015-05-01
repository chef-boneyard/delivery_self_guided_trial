# Delivery Self Guided Trial
Welcome to the Delivery Self Guided Trial

Delivery Trials are invite only and require a license key to complete the install, so if you stumble here on your own please request an [INVITE](https://www.chef.io/delivery/).

These docs will guide you through setting up delivery and configuring pipelines once it is setup. You will install the delivery cluster on your own infrastructure using chef provisioning and your license key. We currently support two install methods. The first is AWS. Using this method provisioning will take care of creating all the resources and setting them up. The second is SHH. This method is used in all other environments and assumes you have created machines and have ssh access with passwordless SUDO on the boxes.

An important consideration in picking your install method/location is network access. If you will be integrating with any apis make sure you can access them from the environment you choose to install delivery in. Often times we setup a cluster only to find an internal api we want hit is not available. Think things like Jenkins or your own internal deployment tool, etc.

## Installation
1. Pick your install path and follow the appropriate doc below:
  * [AWS BASED INSTALL](AWS.md)
  * [SSH BASED INSTALL](SSH.md)

## Setup
