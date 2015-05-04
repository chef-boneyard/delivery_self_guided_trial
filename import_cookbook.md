# Import cookbook

In this example we will import an existing cookbook into Delivery. Do
these steps on your workstation.

1. Make a working directory

        mkdir ~/workspace && cd ~/workspace

2. Setup the delivery-cli config

        delivery setup --server=10.194.9.211 --ent=aws-example --org=sandbox --user=jmorrow

3. Get cookbook source (Pick One)
  * Cookbook hosted in git and has existing delivery config
  
        ```
        git clone https://github.com/opscode-cookbooks/delivery-truck.git
        cd delivery-truck
        ```
    * In this case we are importing from git. Delivery-truck already
      has a delivery config file so the init step below will not
      create a new review. Instead it will just push the project to
      your delivery server and create a pipeline.
    
  * Cookbook hosted in git
  
          ```
          git clone https://github.com/opscode-cookbooks/postfix.git
          cd postfix
          ```
    * This cookbook will fail linting but shows the import process.
    
  * Cookbook in other scm
  
          ```
          Checkout code from SCM
          cd into directory
          remove any scm meta data
          git init
          git add .
          git commit -m 'Initial Commit'
          ```
    * Initializes cookbook as a git repo and creates a master branch
      with an initial commit.
          
  * Cookbook Archive

        ```
        curl -Lo push-jobs.tar https://supermarket.chef.io/cookbooks/push-jobs/download
        tar -xvf push-jobs.tar
        rm push-jobs.tar
        cd push-jobs
        git init
        git add .
        git commit -m 'Initial Commit'
        cd push-jobs
        ```
    * Initializes cookbook as a git repo and creates a master branch
      with an initial commit.
    * This cookbook will fail linting but shows the import process.
    
4. Get a Delivery API token

        delivery token

5. Initialize the cookbook for Delivery

        delivery init
  * Creates a new project in Delivery, pushes the master branch,
    creates a feature branch, generates a default delivery project
    config file, pushes first change for review, and opens browser to
    the change.
  * This sets your new cookbook up to be built with
    [delivery-truck](https://github.com/opscode-cookbooks/delivery-truck). This
    is Chef's opensource build cookbook for chef cookbooks.

#### [Continue in README](README.md)
