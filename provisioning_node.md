# Create Provisioning Node
We use chef-provisioning to create, upgrade, and manage the Delivery Cluster. While it can be done from a workstation, we generally suggest creating a provisioning node for this purpose. This allows you to have a central place from witch to manage the cluster and control who is allowed to manage it.

## Create Node
Use your existing means to provision a new node with one of our supported platforms. This machine does not need to be very powerful since it just runs the provisioning code. In AWS we generally use an t2.micro (Single CPU 2.5GHz, 1 GiB Mem, 8 GiB Disk).

## Setup Provisioning Node
