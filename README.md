# provision-guestshell

This script grew out of an effort to automate enabling Guest Shell on an IOS-XE router. The script is designed to allow for passing session parameters for native access to physical/virtual routers as well as a CSR running as a vagrant box. This is an initial pass at publishing the script. I've outlined my project plan to add functionality here.

# Notes on Running the Script
- Device details are maintained in the device_details.yml
	- Prior to running the script replace any instance of <<text>> with your device specific details.
- Command sets pushed via Netmiko are contained in command_sets.yml.
- You must have a directory titled 'netconf_configs' or the script will fail.
- The script is executed by running provision_gs.py without any additional arguments.

#Caveats
- There is currently an issue with the script if you attempt to run it more than once on the same target. As the script attempts to push out the NAT configuration ncclient generates an error as the configuration already exists. The current work around is to remove the NAT_ACL from the router before running the script again.

# Project Plan
As this is just the initial push of the script I have a short term plan to address the following:

- Leverage getpass to remove the need to statically set the device password in device_details.yml
- Address error generated when a the NAT_ACL already exists on the target device.
- Add framework for updating YUM in Guest Shell, installing git, and populating a repository to be used by Guest Shell.