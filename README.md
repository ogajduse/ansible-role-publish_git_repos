Ansible role for Publishing git repositories on the git mirror
=========

This Ansible role fetches remote git repository and creates mirror on the given system.

Requirements
------------

This role requires properly set up git mirror. For this purpose, please use `install_git_mirror` role.

Role Variables
--------------

This role requires the following variables.

    ssh_pubkeys:
      gitlab.example2.com: |
          gitlab.example2.com ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEAwzZto+U1WUVW8T0xkOyUnDflCBE+G5Men457SXnYon+FY08ksiCvdw8eu7dOuTButxtkBtJ3p/C3OgOUH8wc1UrcFt0ZlaT1Ypt/JSmoUICLfihue6Golon72Ot2IK13LALI0Om+DVh3cqgEUYx/oHu6IvpWmBm2e9cNq1mxbCBu3iO6cvkX8QPYvcyT5Xljf66oCkyIvpO5Bz7j1fNuGAQ009wclNz9XjEiWqZo3UakNEnBCO5eW3vBta1+u1ZM8mBn2YVS/40IbmcVggIg3IpU5LQRI+wQjwP/FfMKo1F8sWOEkm1MJXSBXeUhoetGQIHQXdW3WgIDm0/NDE9KpQ==
          gitlab.example2.com ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBAffh9pq6Ky95ee05hW7wHda57ZfL5Jg7cBjj1szZVeKmEJDkWUBTgibc54ZV2VNiwX50x5BtxiFTH5KqgOJv9o=
          gitlab.example2.com ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAUJMMh5iriY6wt/b78vp++hNWWdeDwXVxUQZquZRedrbJ

    repositories:
      - name: repository_name
        fqdn: gitlab.example.com
        repo_owner: satellite5qe
        clone_user: https

      - name: second_repository_name
        fqdn: gitlab.example2.com
        repo_owner: satelliteqe
        clone_user: git

    repository_destination: "/var/lib/git"
    repository_owner: gitmirror
    repository_group: gitmirror
    repository_mode: 0644

Where `ssh_pubkeys` should hold a public key of every server which is used by the role. Variable `repositories` is an array that consist of required information about the given repositories.

For the first example complete URL should be `https://gitlab.example.com/satellite5qe/repository_name.git` and for the second example the URL should be `git@gitlab.example2.com:satelliteqe/second_repository_name.git`.

The `repository_destination` variable specifies location where the mirrored repositories should be stored. Last three variables specifies repositories owner and group and also mode of the directories located in the `repository_destination`.

Dependencies
------------

This role is not dependent upon any galaxy roles.

Example Playbook
----------------

Here is a simple example of a publish_git_repos_on_mirror role:

    - hosts: servers
      roles:
         - publish_git_repos_on_mirror

License
-------

GNU GENERAL PUBLIC LICENSE

   Version 3, 29 June 2007

Copyright (C) 2007 Free Software Foundation, Inc.

Author Information
------------------

This is developed by Satellite QE team, irc: #robottelo on Freenode
