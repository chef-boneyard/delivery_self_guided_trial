# Create New Cookbook Manual Delivery Steps
In this example we will create a new cookbook, but do all of the delivery steps manually. Run the commands on your workstation.

1. Create project in Delivery
  1. Log into the webui with the admin credentials you got earlier

        cat ~/delivery-cluster/.chef/delivery-cluster-data/aws-example.creds
       
  2. Click 'Organizations' in the left column
  3. Click 'sandbox'
  3. Click the large blue box on left in header
  4. Enter project name (new-project2) and save

2. Setup the delivery-cli config

        delivery setup --server=10.194.9.211 --ent=aws-example --org=sandbox --user=jmorrow

3. Clone project with delivery cli

        delivery clone new-project2
        cd new-project2

3. Create cookbook

        chef generate cookbook .

  * This use chefdk to generate a new cookbook including a defaualt recipe and default chefspec tests

4. Create initial commit

        git add .
        git commit -m 'Initial Commit'
  * Initializes a git repo and creates a master branch with an initial commit.

5. Push master branch

        git push delivery master

6. Create pipeline in Delivery
  1. Log into the webui with the admin credentials you got earlier

        ```
        cat ~/delivery-cluster/.chef/delivery-cluster-data/aws-example.creds
        ```
        
  2. Click 'Organizations' in the left column
  3. Click 'sandbox'
  4. Click 'new-project2'
  5. In the page header click the right small grey box './`\\./'
  6. Enter master for 'Pipeline Name' and master for 'Pipeline Base' and save

7. Initialize the cookbook for Delivery
  1. Create feature branch
  
        ```
        git checkout -b add_delivery_config
        ```

  2. Create config

        ```
        mkdir .delivery
        vi .delivery/config.json
        ```
        
        ```
        {
          "version": "2",
          "build_cookbook": {
            "branch": "master",
            "name": "delivery-truck",
            "git": "https://github.com/opscode-cookbooks/delivery-truck.git"
          },
          "skip_phases": [
            "smoke",
            "security",
            "quality"
          ]
        }
        ```
    * This sets your new cookbook up to be built with [delivery-truck](https://github.com/opscode-cookbooks/delivery-truck). This is Chef's opensource build cookbook for chef cookbooks.
    
8. Add changes to feature branch

        git add .
        git commit -m 'Add delivery config'

9. Submit for Review

        delivery review

#### [Continue in README](README.md)
