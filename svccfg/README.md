SVCCFG Cookbook
==============
 
 	   The svccfg command manipulates data in the service configuration repository.
 	   svccfg can be invoked interactively, with an individual  subcommand, or by 
 	   specifying a command file that contains a series of subcommands.

       Changes made to an existing service in the repository typically do  not
       take  effect  for that service until the next time the service instance
       is refreshed.
 
Requirements
============

     * Chef Client 12.16.42
     * Oracle Solaris 11.3 SRU19


Attributes
==========

Svccfg Cookbook attributes.
---------------------------

<table border="1" bgcolor="#8080cc">
  <tr>
    <th>Key</th>
    <th>Type</th>
    <th>Description</th>
    <th>Default</th>
  </tr>
  <tr>
    <td><tt>name</tt></td>
    <td>String</td>
    <td>name</td>
    <td><tt></tt></td>
  </tr>
   <tr>
    <td><tt>Type</tt></td>
    <td>String</td>
    <td>DataType</td> 
    <td></td>
  </tr>
  <tr>
    <td><tt>fmri</tt></td>
    <td>String</td>
    <td>FMRI</td> 
    <td><tt>Fault Management Resource Identifier</tt></td>
  </tr>
  <tr>
    <td><tt>method_name</tt></td>
    <td>String</td>
    <td>name</td> 
    <td></td>
  </tr>
  <tr>
    <td><tt>options</tt></td>
    <td>Hash</td>
    <td>Key, Value</td> 
    <td>Nil</td>
  </tr>
</table>

Usage
=====
To Create the File
------------------

```ruby
remote_file '/var/tmp/test.xml' do
  source 'http://tycoon.in.oracle.com/files/test.xml'
  owner 'root'
  group 'bin'
  mode '0755'
  action :create
end
```
 Instances it specifies are imported into the repository
 -------------------------------------------------------
```ruby
svccfg 'first-boot' do
  file_name "/var/tmp/test.xml"
  action :import 
end
```

Export Instances
----------------
```ruby 
svccfg 'first-boot' do
  fmri "svc:/site/first-boot"
  file_name "test-out.xml"
  action :export
end
```
To Disable the instances
------------------------

```ruby
svcadm 'first-boot' do
 action :disable
end
```

To Delete the entity specified by fmri
--------------------------------------

```ruby
svccfg 'first-boot' do
 action :delete 
end
```

Sets the name property of the pg property group
-----------------------------------------------
```ruby
svccfg 'system-log' do
   options ({'refresh/timeout_seconds' => '80'})
   action :setprop
end
```
Deletes the named property group 
---------------------------------

```ruby
svccfg 'system-log' do
   options ({'refresh/timeout_seconds' => 'ttttt'})
  action :delprop
end
```

To Add a property group
-----------------------

```ruby
svccfg 'system-log' do
  options ({'test10' => 'application15'}) 
  action :addpg
end
```
To Delete a property group
------------------------
```ruby
svccfg 'system-log' do
  options ({'test10' => 'application5'})
  action :delpg
end
```

Adds the given value to a property
----------------------------------
```ruby
svccfg 'system-log' do
  options ({'config/ven' => 'true'})
  type "boolean"
  action :addpropvalue
end
```
Deletes the named property group
--------------------------------
```ruby
svccfg 'system-log' do
  options ({'config/ven' => 'application5'})
  action :delpropvalue
end
```

Contributing
============

      * Fork the repository on Mercurial
      * Create a named feature branch 
      * Write your Changes
      * Write tests for your change
      * Submit a pull Request Using Mercurial

     
License and Authors
-------------------
```text
- Author:: Pradhap Devarajan ([pradhap.devarajan@oracle.com](mailto:pradhap.devarajan@oracle.com))


Copyright:: 2017 Oracle and/or its affiliates. All rights reserved.

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
