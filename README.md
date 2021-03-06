# Terraform Bluemix SSH Key
A Terraform configuration for creating an [IBM Cloud SSH Key](https://ibm-bluemix.github.io/tf-ibm-docs/tf-v0.9.3-ibm-provider-v0.2.1/r/infra_ssh_key.html) (`ibmcloud_infra_ssh_key`). This will create a SSH key in the specified IBM cloud account.

**This configuration template is written for IBM Cloud Provider version `tf-v0.9.3-ibm-provider-v0.2.1`**

This is not a module, it is a terraform configuration that can be cloned or forked to be used and/or modified with the IBM Cloud terraform binary locally, or it can be used with the [IBM Cloud Schematics](https://console.ng.bluemix.net/docs/services/schematics/index.html#gettingstarted) service.

# Usage with Terraform Binary on your local workstation
You will need to [Setup up IBM Cloud provider credentials](#setting-up-provider-credentials), please see the section titled "[Setting up Provider Credentials](#setting-up-provider-credentials)" for help.

Additionally you will need the [Terraform binary](https://www.terraform.io/intro/getting-started/install.html) and the [IBM Cloud Provider Plugin](https://github.com/IBM-Bluemix/terraform/releases). You can obtain this binary by visiting [github.com/IBM-Bluemix/schematics-onboarding](https://github.com/IBM-Bluemix/schematics-onboarding#ibm-bluemix-schematics-service-on-boarding) and follow the instructions at [https://ibm-bluemix.github.io/tf-ibm-docs#developing-locally](https://ibm-bluemix.github.io/tf-ibm-docs/tf-v0.9.3-ibm-provider-v0.2.1/#developing-locally).

To run this project execute the following steps:

- Supply `datacenter`, `public_key`, `key_label`, and `key_note` variable values in `terraform.tfvars`, see https://www.terraform.io/intro/getting-started/variables.html#from-a-file for instructions.
  - Alternatively these values can be supplied via the command line or environment variables, see https://www.terraform.io/intro/getting-started/variables.html.
- Specifically for `public_key` material see ["Generating a new SSH key and adding it to the ssh-agent"](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/)) so that your workstation will use the key.
- `terraform plan`: this will perform a dry run to show what infrastructure terraform intends to create
- `terraform apply`: this will create actual infrastructure
  - Infrastructure can be seen in IBM Bluemix under the following URLs:
    - SSH keys: https://control.bluemix.net/devices/sshkeys
- `terraform destroy`: this will destroy all infrastructure which has been created

# Available Data Centers
Any of these values is valid for use with the `datacenter` variable:
- `ams01`: Amsterdam 1
- `ams03`: Amsterdam 3
- `che01`: Chennai 1
- `dal01`: Dallas 1
- `dal10`: Dallas 10
- `dal12`: Dallas 12
- `dal02`: Dallas 2
- `dal05`: Dallas 5
- `dal06`: Dallas 6
- `dal07`: Dallas 7
- `dal09`: Dallas 9
- `fra02`: Frankfurt 2
- `hkg02`: Hong Kong 2
- `hou02`: Houston 2
- `lon02`: London 2
- `mel01`: Melbourne 1
- `mex01`: Mexico 1
- `mil01`: Milan 1
- `mon01`: Montreal 1
- `osl01`: Oslo 1
- `par01`: Paris 1
- `sjc01`: San Jose 1
- `sjc03`: San Jose 3
- `sao01`: Sao Paulo 1
- `sea01`: Seattle 1
- `seo01`: Seoul 1
- `sng01`: Singapore 1
- `syd01`: Sydney 1
- `syd04`: Sydney 4
- `tok02`: Tokyo 2
- `tor01`: Toronto 1
- `wdc01`: Washington 1
- `wdc04`: Washington 4

# Running in Multiple Data centers
Simply run `terraform plan -var 'datacenter=lon02' -state=lon02.tfstate` or whatever your preferred datacenter is (replace `lon02` for both arguments), and repeat for `terraform apply` with the same arguments.

# Setting up Provider Credentials
To setup the IBM Cloud provider to work with this example there are a few options for managing credentials safely; here we'll cover the preferred method using environment variables. Other methods can be used, please see the [Terraform Getting Started Variable documentation](https://www.terraform.io/intro/getting-started/variables.html) for further details.

## Environment Variables using IBMid credentials
You'll need to export the following environment variables:

- `TF_VAR_bxapikey` - your Bluemix API Key
- `TF_VAR_slusername` - your Softlayer username
- `TF_VAR_slapikey` - your Softlayer username
- `TF_VAR_slaccountnum` - the target softlayer account number (while optional, it is REQUIRED if you have multiple accounts associated with your ID; otherwise you will recieve an error similar to `* ibmcloud_infra_virtual_guest.debian_small_virtual_guest: Error ordering virtual guest: SoftLayer_Exception_Public: You do not have permission to verify server orders. (HTTP 500)`)

On OS X this is achieved by entering the following into your terminal, replacing the `<value>` characters with the actual values (remove the `<>`:

- `export TF_VAR_bxapikey=<value>`
- `export TF_VAR_slusername=<value>`
- `export TF_VAR_slapikey=<value>`
- `export TF_VAR_slaccountnum=<value>`

However this is only temporary to your current terminal session, to make this permanent add these export statements to your `~/.profile`, `~/.bashrc`, `~/.bash_profile` or preferred terminal configuration file. If you go this route without running `export ...` in your command prompt, you'll need to source your terminal configuration file from the command prompt like so: `source ~/.bashrc` (or your preferred config file).

# Authors
[Chris Kelner](http://github.com/ckelner)

# License
MIT; see [LICENSE](LICENSE) for details.
