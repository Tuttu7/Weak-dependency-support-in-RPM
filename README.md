
```
	rpm -qa --recommends  #list capabalilities ( package names or what they provides )

	rpm -q --whatrecommends #show packages that is recommended
```


#### Weak Dependencies ( Direct )

#### The pacakge recommendeds another packages , weak dependencies are additional packages in an application. By default yum 
#### installs all additional packages if it is not available , yum simply ignores them.

#### Let's see the Weak Dependencies in httpd package 

```
	[root@ip-172-31-31-156 ~]# yum install httpd
	Updating Subscription Management repositories.
	Unable to read consumer identity

	This system is not registered with an entitlement server. You can use subscription-manager to register.

	Red Hat Enterprise Linux 9 for x86_64 - AppStream from RHUI (RP  49 MB/s |  23 MB     00:00    
	Red Hat Enterprise Linux 9 for x86_64 - BaseOS from RHUI (RPMs)  42 MB/s |  13 MB     00:00    
	Red Hat Enterprise Linux 9 Client Configuration                  29 kB/s | 3.2 kB     00:00    
	Dependencies resolved.
	================================================================================================
	 Package                Arch       Version                 Repository                      Size
	================================================================================================
	Installing:
	 httpd                  x86_64     2.4.53-11.el9_2.5       rhel-9-appstream-rhui-rpms      53 k
	Installing dependencies:
	 apr                    x86_64     1.7.0-11.el9            rhel-9-appstream-rhui-rpms     127 k
	 apr-util               x86_64     1.6.1-20.el9_2.1        rhel-9-appstream-rhui-rpms      97 k
	 apr-util-bdb           x86_64     1.6.1-20.el9_2.1        rhel-9-appstream-rhui-rpms      14 k
	 httpd-core             x86_64     2.4.53-11.el9_2.5       rhel-9-appstream-rhui-rpms     1.5 M
	 httpd-filesystem       noarch     2.4.53-11.el9_2.5       rhel-9-appstream-rhui-rpms      17 k
	 httpd-tools            x86_64     2.4.53-11.el9_2.5       rhel-9-appstream-rhui-rpms      87 k
	 mailcap                noarch     2.1.49-5.el9            rhel-9-baseos-rhui-rpms         35 k
	 redhat-logos-httpd     noarch     90.4-1.el9              rhel-9-appstream-rhui-rpms      18 k
	 Installing weak dependencies:
	 apr-util-openssl       x86_64     1.6.1-20.el9_2.1        rhel-9-appstream-rhui-rpms      16 k
	 mod_http2              x86_64     1.15.19-4.el9_2.4       rhel-9-appstream-rhui-rpms     153 k
	 mod_lua                x86_64     2.4.53-11.el9_2.5       rhel-9-appstream-rhui-rpms      63 k
```
	 

  #### Installing httpd without weak dependencies
  
  ```
	 
	 [root@ip-172-31-31-156 ~]# yum install httpd --setopt=install_weak_deps=False 
	Updating Subscription Management repositories.
	Unable to read consumer identity

	This system is not registered with an entitlement server. You can use subscription-manager to register.

	Last metadata expiration check: 0:02:28 ago on Sun 16 Jul 2023 02:59:31 AM UTC.
	Dependencies resolved.
	================================================================================================
	 Package                Arch       Version                 Repository                      Size
	================================================================================================
	Installing:
	 httpd                  x86_64     2.4.53-11.el9_2.5       rhel-9-appstream-rhui-rpms      53 k
	Installing dependencies:
	 apr                    x86_64     1.7.0-11.el9            rhel-9-appstream-rhui-rpms     127 k
	 apr-util               x86_64     1.6.1-20.el9_2.1        rhel-9-appstream-rhui-rpms      97 k
	 apr-util-bdb           x86_64     1.6.1-20.el9_2.1        rhel-9-appstream-rhui-rpms      14 k
	 httpd-core             x86_64     2.4.53-11.el9_2.5       rhel-9-appstream-rhui-rpms     1.5 M
	 httpd-filesystem       noarch     2.4.53-11.el9_2.5       rhel-9-appstream-rhui-rpms      17 k
	 httpd-tools            x86_64     2.4.53-11.el9_2.5       rhel-9-appstream-rhui-rpms      87 k
	 mailcap                noarch     2.1.49-5.el9            rhel-9-baseos-rhui-rpms         35 k
	 redhat-logos-httpd     noarch     90.4-1.el9              rhel-9-appstream-rhui-rpms      18 k

	Transaction Summary
	================================================================================================
	
 Install  9 Packages

```

#### RPM Forward query & Backward query method

```

	RPM forward query for package build from package provider ( redhat )

	[root@ip-172-31-31-156 ~]# rpm -q --recommends apr-util
	apr-util-openssl(x86-64) = 1.6.1-20.el9_2.1


	RPM backward query related to packages from third party vendors 

	[root@ip-172-31-31-156 ~]# rpm -q --whatrecommends 'apr-util-openssl(x86-64)'
	apr-util-1.6.1-20.el9_2.1.x86_64

```



	#### To see packages that are suggested by another packages 

 ```

	[root@ip-172-31-31-156 ~]# rpm -qa --suggests
	glibc-minimal-langpack = 2.34-60.el9
	font(dejavusansmono)
	glibc-doc
	cronie
	xfsprogs-xfs_scrub
	fprintd-pam
	oddjob-mkhomedir
	samba-winbind
	sssd
	systemd-bootchart
	memstrack
	NetworkManager
	selinux-policy-targeted
	gnupg2-smime
	pcsc-lite-ccid
	pinentry
	realmd
	samba-winbind
	sssd
	ntp-refclock

```

####	To see what package suggested sssd

	```
 [root@ip-172-31-31-156 ~]# rpm -q --whatsuggests sssd
	authselect-1.2.6-1.el9.x86_64
	authselect-compat-1.2.6-1.el9.x86_64
 ```

