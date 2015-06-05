# Delivery Self Guided Trial

Welcome to the Delivery Self Guided Trial

Delivery Trials are currently invite only. If you've stumbled here on
your own, please request an [INVITE](https://www.chef.io/delivery/) or 
speak with your Chef account representative.

These docs will provide you with instructions for accessing your trial
environment, and guide you through pushing changes through the delivery
pipeline. Accessing the environment will require internet access, as well
as an SSH client.

## Components
* Workstation Server / Proxy Bastion
    - This machine serves both as your working environment for pushing
    changes through delivery and as a proxy host for accessing the rest
    of the cluster.
* Delivery Server
    - Where the magic happens! This is your target for cloning repositories,
    pushing changes, and has a web-accessible UI.
* Chef Server
    - You will have UI access to the Chef Server to inspect policy and node state
    as well as track the reporting output for your changes.
* Delivery Infrastructure
    - Build Nodes
        - Not accessible via SSH or Web, but these are the machines your delivery
        jobs will run from.
    - Each deployable stage of delivery has its own web-accessible server you can
    use to validate changes you push through the pipeline. Servers are as follows:
        - Acceptance
        - Union
        - Rehearsal
        - Delivered

## Setup Documents
1. Workstation Setup
    * [Log into your workstation, and set up a SOCKS proxy](simple_proxy_workflow.md)
2. Configure Your Workspace
    * [Clone a project, and create a new change](simple_cookbook_workflow.md)
3. Push a Change Through Delivery
    * [Working with the Delivery UI](simple_UI_workflow.md)

## LICENSE AND AUTHORS
- Author: Jon Morrow (<jmorrow@chef.io>)
- Author: Salim Afiune (<afiune@chef.io>)
- Author: Bakh Inamov (b@chef.io)
- Author: Nick Rycar (rycar@chef.io)

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
