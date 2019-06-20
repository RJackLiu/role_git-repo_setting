Role Name
=========

role_git-project_setting
ROLE_ID: '0x01'

Requirements
------------

Packages on control nodes:
- git 
- ansible


Role Variables
--------------

# if true, ansible will cover project paths whether is existed or not.
folder_create_force: false

github_username: ''
github_password: ''

# project_folder_path_in_role:    # change contents or replace with [].
#   - path: '/path/to/yourProjectName01'
#     remote_sync: false          # if false, "url" can be omitted or ignored.
#     url: 'https://github.com/owner/yourPojectName01.git'
#   - path: '/path/to/yourProjectName02'
#     remote_sync: false
#     url: 'git@github.com:owner/yourProjectName02.git'
project_folder_path_in_role:    
  - path: /home/{{ ansible_user }}/git/ansibleRole01
    remote_sync: false
    url: 'https://github.com/owner/yourPojectName01.git'
    git_clone: true

# project_folder_path_n_in_role:    # change contents or replace with [].
#   - path: /path/to/yourProjectName03
#     remote_sync: true             # if false, "url, git_clone" can be omitted or ignored.
#     url: 'https://github.com/owner/yourPojectName03.git'
#     version: HEAD    # Reference Ansible module: git, parameters: version
#     git_clone: true    # if false, git project will be created by "git init"
#   - path: /path/to/yourProjectName04
#     remote_sync: true
#     url: 'git@github.com:owner/yourProjectName04.git'
#     git_clone: false
project_folder_path_n_in_role:
  - path: /home/{{ ansible_user }}/git/project01
    remote_sync: false
    url: 'https://github.com/owner/yourPojectName02.git' 
    git_clone: true

# For git_config module
# git_configuration:    # change contents or replace with [].
#   - name: 'user.name'
#     scope: global    #choices: local / global / system
#     value: 'yourName'
#   - name: 'user.email'
#     scope: global
#     value: 'yourEmail'
#   - name: 'http.sslVerify'
#     scope: global
#     value: false
#   - name: 'user.name'
#     scope: local
#     repo: '/path/to/yourProjectName01'
#     value: 'yourName'
git_configuration:
  - name: 'user.name'
    scope: global
    value: "{{ ansible_user }}"
  - name: 'user.email'
    scope: global
    value: "{{ ansible_user }}@{{ inventory_hostname }}"

Dependencies
------------

none

Example Playbook
----------------

---
- hosts: all
  gather_facts: no
  become: no
  roles:
    - role: role_git-project_setting
      github_username: ''
      github_password: ''
      project_folder_path_n_in_role:
        - path: /home/{{ ansible_user }}/git/project01
          remote_sync: false
          url: 'https://github.com/owner/yourPojectName02.git' 
          git_clone: true
      project_folder_path_n_in_role:
        - path: /home/{{ ansible_user }}/git/project01
          remote_sync: false
          url: 'https://github.com/owner/yourPojectName02.git' 
          git_clone: true
      git_configuration:
        - name: 'user.name'
          scope: global
          value: "{{ ansible_user }}"
        - name: 'user.email'
          scope: global
          value: "{{ ansible_user }}@{{ inventory_hostname }}"
        
License
-------

BSD

Author Information
------------------

Jack Liu
