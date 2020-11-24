# Provisioning A Dev Environment With Vagrant And Virtual Machines

Provisioning helps determine what will be done on the VM by default (.e.g. install relevant programs when turning the machine on for the first time) by giving certain instructions.


## Checking And Installing Required Plugins

* Insert this section of code at the beginning of the `Vagrantfile`:
	* Initiates a variable `required_plugins`, which is then iterated over it to install them
```ruby
# Install required plugins
# this list can contain many plugins
required_plugins = ["vagrant-hostsupdater"]
required_plugins.each do |plugin|
    exec "vagrant plugin install #{plugin}" unless Vagrant.has_plugin? plugin
end
```

## Uploading Files

* Don't need to use rsync or something similar, vagrant comes with a built in option:
```
vagrant upload source destination
```
