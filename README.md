# ansible-ios-oneshot

A playbook which you supply hostnames and config, to push out config once on bulk.

All the data is static to my development environment but you can use this as an example of the logic.

## Aims

Take the input of a csv and generate a hosts file, which you then use to push config.

Workflow:
 - Verify Serial Number, gracefully exit if this doesn't match.
 - Run a show command on the thing you want to push, and exit if you match.
 - Backup before you make a change, optional.
 - Push the change.
 - Save when modified.
 - Backup after the change is complete, optional.

Most of the above will need to be broken out into roles, but that will come at a later date.

## Example of how to run
This play is work in progress, so not all of the features are complete.
ansible-playbook oneshot.yml -vv --tags "show"

## CSV File
CSV format to generate the data:

Host part of the CSV.
This is what every host needs to just exist.
SERNO is the serial of the chassis, as there are plenty of parts with a number. This has to be produced before the play is run otherwise it will fail. 

I really want the ability to check the host you are about to work on tally's up with serial number for that host.

host;ansible_ssh_host;os;serno
csr1;192.168.178.85;IOS;9HGPHTOFJIH;


List out the checks you wish to perform before applying code:
check1;check2;check3
"show inventory";"show run | i hostname";show run interface gigabitEthernet1"

The details for the config to apply.
This produces a set of data, tied to the parent, and the lines being a list which must be under the parent. Checkout the lists page in ansible docs.

parent;lines;
"interface gigabitEthernet4";["description Hello World","ip address 1.1.1.1 255.255.255.0"]

Ideally, you would have a hosts_var file per host, but this way, we generate all the data into one file, the inventory file. But this concept can be adapted.

## To Do ##
Get the list format working in the test.
Test the SERNO check, as I'm just paranoid.
Also check the hostname matches.
Jinja2 template to build out the inventory file.
Roles after that