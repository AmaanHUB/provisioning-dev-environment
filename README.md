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

* Or just use `bundle` if there is a `Gemfile` present, as this will automatically parse it and install them
	* Will install them system-wide unless otherwise specified

## Ruby's Testing Framework (RSpec)

* Install bundler first (don't forget to add gems/ruby to $PATH first if it hasn't automatically)
```
gem install bundler
```
* Install with a Bundler
* Creates a Rakefile, can use to say which tests to run and when (from the a something.rb file)
	* Run with `rake spec` to run the tests
	* It can check within and outside the virtual machine

## JS Package Manager

* NPM (Node Package Manager)
	* JS comes pre-loaded after a certain version)
