# Create and Import cookbook

In this example we will create a new cookbook and import it into
Delivery. Do these steps on your workstation.

1. Make a working directory

        mkdir ~/workspace && cd ~/workspace

2. Setup the delivery-cli config

        delivery setup --server=10.194.9.211 --ent=aws-example --org=sandbox --user=jmorrow

3. Create Cookbook

        chef generate cookbook new-cookbook
        cd new-cookbook
  * This use ChefDK to generate a new cookbook including a default
    recipe and default ChefSpec tests

4. Create initial commit

        git add .
        git commit -m 'Initial Commit'
  * Initializes a git repo and creates a master branch with an initial
    commit.

3. Get a Delivery API token

        delivery token

4. Initialize the cookbook for Delivery

        delivery init
  * Creates a new project in Delivery, pushes the master branch,
    creates a feature branch, generates a default Delivery project
    config file, pushes first change for review, and opens browser to
    the change.
  * This sets your new cookbook up to be built with
    [delivery-truck](https://github.com/opscode-cookbooks/delivery-truck). This
    is Chef's open-source build cookbook for chef cookbooks.

#### [Continue in README](README.md)
