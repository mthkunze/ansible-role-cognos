IBM Cognos PowerPlay Server
=========
Ansible Role to install IBM Cognos 

Requirements
------------
You need a copy of Cognos compressed in your preferred Version. The Tarball Package can download from a remote URL or use a local copy of Cognos Packages present on your ansible host.

root is necessary!
------------

This role can only be used with root access. Cognos could not be installed without root but many features configurations like creating configurations
are available as run owner, if remote access is allowed. Make sure you're installing with root user or using privillege escalation with sudo is given.

    Example:
        /etc/group > wheel:x:10:remoteuser
        /etc/sudoers > %wheel	ALL=(ALL)	NOPASSWD: ALL


Role Variables
--------------

Cognos_BINARY
------------


This hash controls how to send the Cognos binary to the remote hosts.

cognos_binary.url: A url to download cognos (don't set this if you want to use a local copy)
cognos_binary.location: A path to save the remote file or to get the file if url wasn't defined
cognos_binary.dest: Where the role should decompress Cognos Package on remote host.

    cognos_binary:
        url: https://fileserver/downloads/bi_svr_10.2.2_l86_ml.tar.gz
        location: /opt/ibm/insttemp/bi_svr_10.2.2_l86_ml.tar.gz
        dest: /opt/ibm/insttemp


Cognos_PACKAGES
------------

The list of packages that the role should install before running the installer. Leave as default unless you know what you're doing.

Cognos requires some packages to run properly on Linux, you can read more about this 
http://www-969.ibm.com/software/reports/compatibility/clarity-reports/report/html/softwareReqsForProduct?deliverableId=1410436098512&osPlatform=Linux


    Required patches:

        glibc-2.12-1.80.el6 (both i686 and x86_64 packages) - 32 and 64 bit glibc libraries
        libstdc++-4.4.6-4.el6 (both i686 and x86_64 packages) - 32 and 64 bit libstdc++ libraries
        nspr-4.9-1.el6 (both i686 and x86_64 packages) - 32 and 64 bit nspr library for CAM ldap provider
        nss-3.13.3-6.el6 (both i686 and x86_64 packages) - 32 and 64 bit nss library for CAM ldap provider
        openmotif-2.3.3-4.el6 (both i686 and x86_64 packages) - 32 and 64 bit openmotif libraries 

Cognos Response File. You will find it after Decompressing in the SUB-Directory linuxi38664h as response.ats 
------------


Choose your configuration from this Response Files Value Table

    --------- 
    [Dialog1]
    Title=Welcome to the Installation Wizard
    DE=0
    EN=1
    [Dialog2]
    Title=IBM License Agreement
    I Agree=y
    [Dialog3]
    Title=Non IBM License Agreement
    I Agree=y
    [Dialog4]
    Title=Installation Location
    APPDIR=/opt/cognos
    BACKUP=1
    PRODUCTION_RADIO=1
    [Component List]
    C8BISRVR_APP=0
    C8BISRVR_APPLICATION_TIER=0
    C8BISRVR_GATEWAY=0
    C8BISRVR_CONTENT_MANAGER=0
    C8BISRVR_CONTENT_DATABASE=0
    ----------

This hash is used to customize the Cognos installation.

Dialog1: Witch language will be installed
Dialog2: Accept or decline the license (If decline the Cognos won't be installed)
Dialog3: Accept or decline the non IBM license (If decline the Cognos won't be installed)
Dialog4: Choose install location
CompList: Choose Cognos Components

    resp:
       Dialog1: "DE=1"
       Dialog2: "I Agree=y"
       Dialog3: "I Agree=y"
       Dialog4: "APPDIR=/opt/ibm/cognos/"
       CompList: "C8BISRVR_APP=0"


Dependencies
------------
None

Example Playbook
----------------
None

You need at least specify where to get Cognos. Downloading cognos....

    - hosts: server
      roles:
         - cognos
      vars:
        cognos_binary:
          location: /opt/ibm/insttemp/cognos_10.5.tar.gz
           dest: /opt/ibm/insttemp

### Creating a Cognos Framework

The instance will be created using all Cognos defaults, but you can customize it using the hash **cognos_instances**

    cognos_instances:
         - instance: "cognos"
           name: "myinstan" 
           group_name: "myinadm"
           
### Customizing Parameters

Global Instance Configuration for Cognos Instances and Software Parts can be customized.

Define hash `cognos_params` and set any `key: value` Cognos parameter. The key must be a valid Cognos parameter.

    cognos_instances:
        - instance: "cognos"
          name: "rc.cognos" 
          path: "/etc/init.d/cognos_cm"
            
The full example [here](https://github.com/mthkunze/ansible-role-cognos/tree/master/examples/instance_with_custom_params.yml)


Disclaimer
---------
There still some work to be done. Tested with Cognos V10.5. Newer Versions need customizing. There's no warranty that the role will work for you.

License
-------
BSD

Author Information
------------------
Martin Kunze > https://github.com/mthkunze
