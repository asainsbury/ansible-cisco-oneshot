# ansible-ios-oneshot

> # **one-shot**
> adjective NORTH AMERICAN informal\
> achieved with a single attempt or action.\
> "there is no one-shot solution to the problem"\
> done, produced, or occurring only once.\
> "a one-shot deal"

The playbook takes the input from a csv file containing hosts and commands, and converts it into a host inventory file which is used to push config out on mass. 

I'm working on not making the variables static, and converting this into a role, which can be downloaded in Galaxy.

## Workflow:
 - Verify Serial Number, hostname and Software type, and gracefully exit if this doesn't match.

 - Push the change.
 - Save when modified.

### On the to do list:
 - Run a show command on the thing you want to push, and exit if you match.
 - Backup before you make a change, optional.
 - Backup after the change is complete, optional.
Most of the above will need to be broken out into roles, but that will come at a later date.

## Example of how to run
This play is work in progress, so not all of the features are complete.

`ansible-playbook oneshot.yml -vv --tags "gen_hosts"`\
`ansible-playbook oneshot.yml`\

## CSV Format
inventory_hostname| ansible_ssh_host | ansible_ssh_port | serno | type | parent | line1 | line2
----- | ----------| -------| --------| -----| --------------------------| -------------------| ----------------
csr1|127.0.0.1|2221|9HGPHTOFJIH|IOS|interface GigabitEthernet1|description Hello World|ip address dhcp


