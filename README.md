squid
=====

<img src="https://docs.ansible.com/ansible-tower/3.2.4/html_ja/installandreference/_static/images/logo_invert.png" width="10%" height="10%" alt="Ansible logo" align="right"/>

Installs and configures squid with templating of the most common set of parameters.

Current version available on your platform only (no upgrade from an existing installation)

Requirements
------------

None

Role Variables
--------------

__Defaults__
Common configuration
- `squid_cache_mgr` : cache manager's email ; defaults to `squid@example.com`
- `squid_http_port` : port to which squid listens ; defaults to `3128`
- `squid_error_default_language` : defaults to `en`

Access list definition
- `squid_acl_list` : list of acls ; default `localnet` set to RFC1918 possible internal network and localhost - __edit depending on your needs__

Access control
- `squid_http_access_rules` : list of acls that are allowed or denied access to the proxy ; defaults to `allow localnet`
- `squid_acl_safe_ports` : ports the proxy is allowed to connect to ; defaults to most used ports on the Internet (same as squid's default configuration)
- `squid_acl_ssl_ports` : ports to which the CONNECT command is allowed to ; defaults to `443` (same as squid's default configuration)

Cache control
- `squid_cache_dir_size` : size of default disk cache ; `undefined` by default ; example show how to set it to 256 MB
- `squid_maximum_object_size` : maximum size of file stored in the cache ; defaults to `4 MB` (squid default)
- `squid_cache_list`: additional 'cache' directives, used to explictely allow or deny caching of requests matching the acl ; defaults to `[]` (empty)

Cache peer control
- `squid_cache_peers` : list of cache peers ; defaults to `[]` (empty) ; for the ones with authentication please use a secrets environment file
- `squid_cache_peer_access_rules` : list of cache_peer with the acl allowed or denied to use the cache peer ; defaults to `[]` (empty) ; example includes the use of `squid_always_direct_rules` 
- `squid_always_direct_rules` : prevent any cache_peer being used for requests matching the acls ; defaults to `[]` (empty)
- `squid_never_direct_rules` : always use cache peers for requests matching the acls (those defined with `squid_always_direct_rules` take precedence) ; defaults to `[]`

__Vars__  
- `squid_user` : UNIX user squid runs as ; platform-dependent, defaults to `squid`
- `squid_group` : UNIX group squid runs as ; platform-dependent, defaults to `squid`

__Globals__  
None

Dependencies
------------

None

Compatibility
-------------

This role has been tested on these platforms :  
|Distribution|Version|
|------------|-------|
|Debian|10 (buster)|
|Debian|9 (stretch)|
|Amazon Linux|2 (karoo)|

Ansible version :  
* 2.9 : 2.9.0 ; python3 (3.7.5)

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - role: jcmontigny.ansible_squid

License
-------

BSD

Author Information
------------------

Jean-Christophe Montigny
