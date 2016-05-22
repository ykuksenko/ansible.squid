Role Variables
--------------

Default variables:
 - squid_user: user to set file owner ship and to run squid as (ussually leave as default)
 - squid_group: same as user but the group
 - squid_selinux_state: set the selinux state
 - squid_selinux_policy: set the selinux policy
 - squid_maximum_object_size_in_memory: max size of an object to keep in RAM
 - squid_maximum_object_size: set the max size of a file that squid will cache (according to the refresh patterns)
 - squid_cache_dir: sets up one or more directories to use as squid cache has three options
   - dir: path to where the cache should be created
   - type: squid cache type (see squid.conf manual)
   - options: options specific to the squid cache type (see squid.conf manual)
 - squid_listen_ip: set the ip to listen on
 - squid_listen_port: set the port to use on the listen ip
 - squid_intercept_ip: set the ip to listen on for intercepted traffic (requires a local nat to work)
 - squid_intercept_port: set the port to listen on for intercepted traffic. If set to 0 this will be disabled.
 - squid_local_subnets: the subnets that squid will accept traffic from
 - squid_nameservers: the name servers squid should use for name resolution

Optional variables:
 - squid_domain_bypass_list: a list of domain that should not be cached by squid but forwarded directly. The syntax is from squid config files so you will need to use a leading dot (.) before the domain you would like to bypass the cache (see the example below) this is optional and will be disabled (omitted) if nothing is set.

Dependencies
------------

python2-firewall package (fedora)

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
        - {role: 'proxy',
           squid_maximum_object_size: '512 KB',
           squid_cache_dir: [{'dir': '/mnt/squid/aufs', 'type':'aufs', 'options': '20000 32 256'}],
           squid_local_subnets: ['192.168.1.0/24','10.10.10.0/24'],
           squid_name_server: ['8.8.8.8','8.8.4.4'],
           squid_domain_bypass_list: ['.domain.com','.google.com'],
          }

License
-------

GPL v3

Author Information
------------------

Yevgeniy Kuksenko
