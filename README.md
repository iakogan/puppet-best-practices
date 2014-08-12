puppet-best-practices
=====================



## Module Composition is important
https://docs.puppetlabs.com/guides/module_guides/bgtm.html


## Use arrows

-> (ordering arrow)

~> (notification arrow)

see more:  https://docs.puppetlabs.com/puppet/3/reference/lang_relationships.html#chaining-arrows


## Use anchor before and after: 

```puppet
class my () {
  anchor { "my::begin": } ->
  class {"my::install": } ->
  class {"my::config": } ~>
  class {"my::service": } ~>
  anchor { "my::end": }
}
```
#

Why? You will be grateful to yourself when you will orchestrate your puppet deployment.  
https://docs.puppetlabs.com/guides/module_guides/bgtm.html#containment-and-anchoring
http://projects.puppetlabs.com/projects/puppet/wiki/Anchor_Pattern



## Use module templates
https://github.com/spiette/puppet-module-skeleton/blob/master/skeleton/manifests/init.pp.erb


## Use *undef* if your default value is unknown
Do not leave it empty string. 


## Use validate_*  functions
```puppet
  validate_absolute_path($config_dir_path)
  validate_bool($config_dir_recurse)
  validate_string($config_file_mode)
```


## Use http://puppet-lint.com/
Prefreably automaticaly. 

## Do NOT do Hiera lookups in your component modules unless it is hiera_hash _with_ merge

## Use The params class pattern
TODO: Class patern goes here

## Use stdlib, it is cool! Do not re-invent!
For example use *file_line* from stdlib when possible not augias
https://forge.puppetlabs.com/puppetlabs/stdlib
TODO: other usefull functions from stdlib

## Document your module. It is easy. 
Use puppet-labs documentation template: 
https://docs.puppetlabs.com/puppet/latest/reference/modules_documentation.html
Git markdown: 
https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet#code


## (TO DISCUSS) We can do ruby code in puppet manifests if future parser is activated 

```
  # grep parser puppet.conf
  parser = future
```
  
  
```puppet
  # now you can loop trough array or hash
  $trusted_networks.each |$network| {
    firewall { "003 allow all traffic from ${network}":
      proto  => 'all',
      source => $network,
      action => 'accept',
    }
  }
```
https://docs.puppetlabs.com/puppet/latest/reference/experiments_future.html



## In verery template or file add a header: 

     # This file is managed by <%= @name %> puppet module! 
     <!- This file is managed by <%= @name %> puppet module!-> 

## Do NOT use exported resources unless you have PuppetDB. 


# More reading: 

http://puppetlabs.com/blog/best-practices-building-puppet-modules
http://projects.puppetlabs.com/projects/1/wiki/Puppet_Best_Practice2
