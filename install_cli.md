## Installing the Delivery CLI
To interact with delivery we suggest you use our cli on your workstation. Currently we support Mac, Ubuntu 14.04, RHEL 6.5, EL 6.5.

##### Mac
1. Download the [package](https://s3.amazonaws.com/delivery-packages/cli/deliverycli-20150415170013-1.pkg).
2. Click the pkg and install

##### Ubuntu
1. ```curl https://packagecloud.io/install/repositories/chef/current/script.deb | sudo bash```
2. ```sudo apt-get install delivery-cli```

##### RHEL/EL (This install is the least tested...)
1. ```curl -o delivery-cli.rpm https://s3.amazonaws.com/delivery-packages/cli/delivery-cli-20150408004719-1.x86_64.rpm```
2. ```sudo yum install delivery-cli.rpm```
