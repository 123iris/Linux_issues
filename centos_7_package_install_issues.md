# Issues while installing yum packages in Centos 7

## 1. Error No package vim Available

### Issue:
```
[root@oNode ~]# yum install vim

Loading mirror speeds from cached hostfile
 * ovirt-4.2-epel: epel.mirror.angkasa.id
No package vim available.
Error: Nothing to do
```

### Solution: 

* Open Centos-Base.repo file and  comment enable=0 or enable=1 and uncomment the baseurl

```
[root@oNode ~]# sudo vi /etc/yum.repos.d/CentOS-Base.repo
[base]
# enabled=0							# comment this
name=CentOS-$releasever - Base
mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os&infra=$infra
baseurl=http://mirror.centos.org/centos/$releasever/os/$basearch/		           # uncomment this
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

#released updates
[updates]
# enabled=0                         # comment this 
name=CentOS-$releasever - Updates
mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=updates&infra=$infra
baseurl=http://mirror.centos.org/centos/$releasever/updates/$basearch/             # uncomment this
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

#additional packages that may be useful
[extras]
# enabled=0                         # comment this 
name=CentOS-$releasever - Extras
mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=extras&infra=$infra
baseurl=http://mirror.centos.org/centos/$releasever/extras/$basearch/             # uncomment this 
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

#additional packages that extend functionality of existing packages
[centosplus]
# enabled=0                  # comment this 
name=CentOS-$releasever - Plus
mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=centosplus&infra=$infra
baseurl=http://mirror.centos.org/centos/$releasever/centosplus/$basearch/         # uncomment this 
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

```

* Now try to install packages

```
[root@oNode ~]# yum install vim -y
Loaded plugins: enabled_repos_upload, fastestmirror, imgbased-persist, package_upload, product-id, search-disabled-repos, 
....
....
Installed:
  vim-enhanced.x86_64 2:7.4.629-8.el7_9                                                                                                       

Dependency Installed:
  gpm-libs.x86_64 0:1.20.7-6.el7            vim-common.x86_64 2:7.4.629-8.el7_9            vim-filesystem.x86_64 2:7.4.629-8.el7_9           

Complete!
```