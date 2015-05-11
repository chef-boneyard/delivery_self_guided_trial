# Notes On Consolidated Install

I have been able to get Delivery running on a consolidated footprint:

### Delivery Server/Builder/Provisioning all one node
Because we set up the node as a provisioning node we install chefdk this means when provisioning comes back to
setup the node the omnibus install of chef is not there. For now the fix is to install the omnibus chef on the
provisioning node in addition to the chefdk. Bug is filed to fix. This only comes up when a provisioning node
is also a builder.
