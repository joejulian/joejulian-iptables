#Puppet iptables module

This puppet module installs an iptables configuration, suitable for loading via the standard service routines.

##Usage:
###Resource:
1. Install this module
1. Load the rule in the resource it affects
  ```puppet
  include "iptables::resource"

  iptables::resource { 'webserver1_web':
          port     => ["80","443"],
  }
  ```
1. Optional Parameters:
 1. 'table': filter,nat,mangle,raw,{user defined}. default: mangle
 1. 'protocol': tcp,udp,udplite,icmp,esp,ah,sctp or all. default: ["tcp","udp"]
 1. 'not_protocol': tcp,udp,udplite,icmp,esp,ah,sctp or all. default: undef
 1. 'source': source address. default: undef
 1. 'not_source': source address. default: undef
 1. 'destination': destination address. default: undef
 1. 'not_destination': destination address. default: undef
 1. 'jump': jump target. default: undef
 1. 'goto': goto chain. default: undef
 1. 'in-interface': interface via which packet was received. default: undef
 1. 'not_in-interface': interface via which packet was received. default: undef
 1. 'not_out-interface': interface via which packet will be sent. default: undef
 1. 'fragment': true,false,undef. default undef
 1. 'not_fragment': true,false,undef. default undef
 1. 'set_counters': initialize counter

* See iptables man page for the match and target extensions. Prepend 'not_' if the extensions supports the negative.

###Node:

1. In the node definition
```puppet

  class { "iptables":   }
  ```
1. Optional boolean parameter 'reload' can be reset to prevent iptables from being reloaded in the event of a configuration change. This would cause the rules to only be loaded at installation time and on subsequent boots.

Caveats:
--------
* This is designed for RHEL/CentOS/Fedora(<18). Will need help testing on other platforms.
