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

* Sync a folder or file with the VM on startup
	* Changes in one makes changes in other :)
```ruby
  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  config.vm.synced_folder "./app", "/app"
```

* Don't need to use rsync or something similar, vagrant comes with a built in option:
```
vagrant upload source destination
```

## Gems And Bundler Vs Pip And Packages

* Gems are packages in Ruby or dependencies
* Bundler is Ruby's package manager
* Gemfile keeps a list of dependencies to be installed (like requirements.txt file in Python)
* To install gens from the Gemfile, you run:
```
bundle install
```

## Ruby's Testing Framework (RSpec)

* Install with a Bundler

## JS Package Manager

* NPM (Node Package Manager)
