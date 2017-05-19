# Chef Cookbooks For Oracle Solaris
Chef Cookbooks to automate administration of Oracle Solaris.

# Chef Cookbooks Overview
   - beadm, Solaris Boot Environments management

# Getting Started
   - Oracle Solaris 11.3 release
   - [Chef Client](https://downloads.chef.io/chef/12.19.36#solaris2), can be installed
     manually or via Omnitruck installer
   - Chef Server to push cookbooks to client nodes (with Chef Client installed)
   - Make sure to pass appropriate arguments in your cookbook/recipe
   - Refer to documentation of individual cookbooks for various options
     and arguments supported by each cookbook
   - No additional setup or configuration is required

# Testing Cookbooks With Chef Development Kit (ChefDK)

If you are testing cookbooks with ChefDK:
   - Download ChefDK from https://downloads.chef.io/chefdk
   - Prepare Solaris vagrant image follow https://www.vagrantup.com/docs/boxes/base.html
   - Upload the cookbooks to ~/cookbooks directory 
   - Run the cookbooks by enabling it in .kitchen.yml.

By default ~/cookbooks directory is used. If you use a non-default directory update
.kitchen.yml with add 'cookbook_path: "test/cookbooks"' in suites section.

```text
  name: vagrant

provisioner:
  name: chef_solo
  no_proxy: localhost,127.0.0.1

verifier:
  name: busser

network:
      - ["private_network"]
      - ["private_network"]

platforms:
   - name: solaris

suites:
  - name: default
    run_list:
      - recipe[deploy-cookbook::default]
```

# Limitations
The Chef cookbooks were created for use in Oracle Solaris 11.3 release.

# Contributing
This project is an open source project. See [CONTRIBUTING](./CONTRIBUTING.md) for details.

Oracle gratefully acknowledges the contributions to open source projects that have been made by the community.

# License
Copyright (c) 2017, Oracle and/or its affiliates. All rights reserved.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

See [LICENSE](./LICENSE) for full license agreement.
