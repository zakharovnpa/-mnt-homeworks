root@server1:~/learning-ansible/Lesson-ansible-02/ansible-02-playbook# ansible-lint 4-site.yml 
WARNING  Overriding detected file kind 'yaml' with 'playbook' for given positional argument: 4-site.yml
WARNING  Listing 1 violation(s) that are fatal
risky-file-permissions: File permissions unset or incorrect
4-site.yml:18 Task/Handler: Ensure installation dir exists

You can skip specific rules or tags by adding them to your configuration file:
# .ansible-lint
warn_list:  # or 'skip_list' to silence them completely
  - experimental  # all rules tagged as experimental

Finished with 0 failure(s), 1 warning(s) on 1 files.
