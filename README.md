set_wordpress_permisions
========================

Although WordPress systems can be hacked a variety of ways, a lot of times it simply comes down to the either the site not being properly updated for some time and/or the permissions not being set properly. This role aims to help with reduce the chances of some script kiddie getting access to yours or your clients' WordPress sites by properly setting the Linux file permissions. Additional hardening, monitoring and preventative measures are certainly needed but every little bit helps.

Requirements
------------

Must be hosting on a Linux based system.

Role Variables
--------------

Will you be passing a list of databases and/or database users to setup? Default is `false`, which means that you should make sure that the  `set_wordpress_permissions_subfolder_used_to_serve_files` role variable is set to an applicable value for your site's document root on your webserver. 

```
set_wordpress_permissions_certs_use_list: false
```

The document root for the webserver. The default is `/var/www`. Leave the trailing slash off.

```
set_wordpress_permissions_web_home: "/var/www"
```

The name of the folder created under each website folder that holds the files webserver will serve up.

```
set_wordpress_permissions_subfolder_used_to_serve_files: "www"
```

The structure for passing a list, showing only the *required* fields. The `name` field in the list below is used for storing the name of the folder under the `set_wordpress_permissions_web_home` that stores the users files. The `site_subfolder_used_to_serve_files` field will then be a subfolder under of the `name` folder that will be used by the webserver to serve up the files for the website. Assuming that the `set_wordpress_permissions_web_home` role variable uses the default value of `/var/www`; your web server would expect that one of the sites it hosts to have a document root of `/var/www/customer123/www`

```
set_wordpress_permissions_setup_sites_to_set_up:
  - {
      name: 'customer123',
      site_subfolder_used_to_serve_files: "www"
    }
```

Dependencies
------------

No other dependencies.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```
	- hosts: your_webserver
	  vars_files:
	    - vars/main.yml
	  roles:
	    - stancel.set_wordpress_permisions
```

or just pass the variables in the playbook

```
	- hosts: your_webserver 
	  vars:
        set_wordpress_permissions_setup_sites_to_set_up:
          - {
              name: 'mysite',
              site_subfolder_used_to_serve_files: "current/build/html"
		    }
          - {
              name: 'mysite2',
              site_subfolder_used_to_serve_files: "www"
		    }		
	  roles:
	    - stancel.set_wordpress_permisions
```

License
-------

GPLv3

Author Information
------------------

[Brad Stance](https://github.com/stancel)
