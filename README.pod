vm-rebuild
==========

Use VMware Perl SDK to force PXE rebuild of Virtual Machines

==========

VM-REBUILD(1)         User Contributed Perl Documentation        VM-REBUILD(1)

NAME
       vm-rebuild.pl - Perform OS reinstall for specified Virtual Machines

SYNOPSIS
        vm-rebuild.pl [VMware options] [options]

DESCRIPTION
       This command provides an interface to temporarily adjust the boot order for a virtual machine so it will perform a PXE boot.  It sets the boot device to ’net’, instructs VMware to reset the Virtual Machine and then sets the boot device back to ’hd’.  This
       requires that a PXE boot environment exists and is configured to perform network-based installations.

VMWARE OPTIONS
       In addition to the command specific options, there are general VMware Perl SDK options that can be used:

       config (variable VI_CONFIG)
           Location of the VI Perl configuration file

       credstore (variable VI_CREDSTORE)
           Name of the credential store file defaults to <HOME>/.vmware/credstore/vicredentials.xml on Linux and <APPDATA>/VMware/credstore/vicredentials.xml on Windows

       encoding (variable VI_ENCODING, default ’utf8’)
           Encoding: utf8, cp936 (Simplified Chinese), iso-8859-1 (German), shiftjis (Japanese)

       help
           Display usage information for the script

       passthroughauth (variable VI_PASSTHROUGHAUTH)
           Attempt to use pass-through authentication

       passthroughauthpackage (variable VI_PASSTHROUGHAUTHPACKAGE, default ’Negotiate’)
           Pass-through authentication negotiation package

       password (variable VI_PASSWORD)
           Password

       portnumber (variable VI_PORTNUMBER)
           Port used to connect to server

       protocol (variable VI_PROTOCOL, default ’https’)
           Protocol used to connect to server

       savesessionfile (variable VI_SAVESESSIONFILE)
           File to save session ID/cookie to utilize

       server (variable VI_SERVER, default ’localhost’)
           VI server to connect to. Required if url is not present

       servicepath (variable VI_SERVICEPATH, default ’/sdk/webService’)
           Service path used to connect to server

       sessionfile (variable VI_SESSIONFILE)
           File containing session ID/cookie to utilize

       url (variable VI_URL)
           VI SDK URL to connect to. Required if server is not present.

       username (variable VI_USERNAME)
           ESXi or vCenter Username

       verbose (variable VI_VERBOSE)
           Display additional debugging information

       version
           Display version information for the script

OPTIONS
       vmname
           Required. The name of the virtual machine. It will be used to select the virtual machine.  Cannot be used in conjunction with the vmname-re option.

       vmname-re
           Required. A Perl regular expression describing the name of one or more virtual machines.  If the regular expression matches multiple Virtual Machines, it will select all matching hosts.  Cannot be used in conjunction with the vmware option.

       out Optional. Filename to which output is written.  If the file option is not suppled, output will only be displayed to the console.

       quiet
           Optional. Suppress console output and assume an affirmative response to all prompts.

PREREQUISITES
       The functionality provided by this command relies on the vSphere Perl SDK for vSphere (https://developercenter.vmware.com/web/sdk/55/vsphere-perl)

EXAMPLES
       Rebuild all ’foo’ Virtual Machines:

        vm-rebuild.pl --vmname-re foo

       Rebuild a single Virtual Machine named ’bar’, send output to ’filename.txt’:

        vm-rebuild.pl --vmname bar -out filename.txt

       Sample Output

        $ vm-rebuild.pl --vmname test-host-1 --out foo.txt
        Looking up VMs: test-host-1
        VM lookup complete
        Rebuilding 1 VM(s)
        Verify that test-host-1 is configured to build on next boot
        Are you sure you want to rebuild test-host-1? y
        Setting netboot for test-host-1
        Rebooting test-host-1
        Virtual Machine ’test-host-1’ on esxi-1.example.com reset successfully
        Restoring boot order for test-host-1

SUPPORTED PLATFORMS
       This command is tested and known to work with vCenter 5.5u1 and ESXi 5.5u1

perl v5.8.8                       2014-06-12                     VM-REBUILD(1)
