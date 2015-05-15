# Workstation Access/Proxy Workflow

This document will walk you through the process of connecting to your workstation node. This server will be used for:
* Creating, testing and staging all of your cookbook changes.
* Creating a SOCKS proxy to access the delivery environment's web UI

## Prerequisites

You will need an interactive SSH client. All work in the guided trial will be done from inside the workstation server. 

## Log in to your workstation

Pretty straightforward! We'll ask that you provide public SSH keys for any users you'd like to have access, and we will add it to the workstation's authorized_keys.

Username: workstation

You will have access to the ChefDK and the Delivery CLI inside of this server.

## Set up a SOCKS Proxy

From a terminal, you can create a tunnel to your workstation server like so:

 ssh -N -D 1080 workstation@[SERVER IP]

From there, most browsers will have an option to set up a SOCKS proxy in their advanced settings.

### For Firefox

* In Preferences, click the "Advanced" tab, and then the "Network" sub-tab.

* Click "Settings" in the "Connections" section. This should pop up a new window.

* Select "Manual Proxy Configuration" and put the following information in "SOCKS Host":
 Host: 127.0.0.1
 Port: 1080

* Click "OK"

### For Chrome
* In Settings, click "Advanced Settings" at the bottom of the page

* In the "Network" section, click "Change Proxy Settings". This will open up your OS's proxy settings.

#### Windows
* Select “Connections”

* Select “LAN Settings”

* Under Proxy server, click to select the Use a proxy server for your LAN check box and click “Advanced”

* In the Socks Proxy Address to use textbox, type 127.0.0.1

* In the Port box, type 1080

* Click OK.

#### MacOS
* Select "SOCKS Proxy"

* In the Address box, type 127.0.0.1

* In the Port box, type 1080

* Click Apply

You should now be able to connect to your Delivery Server, Chef Server, and Nodes via your browser.

#### Continue to the [Local Development Cookbook workflow](simple_cookbook_workflow.md) doc, and let's stage a change for review!

#### Back to the [README](README.md)
