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
 - Backup after the change is complete.

Most of the above will need to be broken out into roles, but that will come at a later date.

## Example of how to run
This play is work in progress, so not all of the features are complete.
ansible-playbook oneshot.yml -vv --tags "show"