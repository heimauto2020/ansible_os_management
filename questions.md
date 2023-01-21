# Ansible Usage:
### Defaults:
Default file:
defaults/main.yml
```
---
# defaults file for os_software
software:
  apt:
    - name: "python3-apt"
    - name: "python3-dev"
    - name: "python3-pip"

  update:
    - test: "pip"
    - test: "pip"
```
### Try 1:
/roles/os_software/tasks/main.yml
main.yml file:
```
---
    - debug:
        msg: "{{ software }}"

    - debug:
        msg: "{{ software['update'] }}"

    - debug:
        msg: "{{ software['apt'] }}"
```
Result:
```
TASK [os_software : debug] *****************************************************************************************************************************
task path: ./roles/os_software/tasks/apt/main.yml:2
ok: [localhost] => {
    "msg": {
        "apt": [
            {
                "name": "python3-apt"
            },
            {
                "name": "python3-dev"
            },
            {
                "name": "python3-pip"
            }
        ],
        "update": [
            {
                "test": "pip"
            },
            {
                "test": "pip"
            }
        ]
    }
}

TASK [os_software : debug] *****************************************************************************************************************************
task path: ./roles/os_software/tasks/apt/main.yml:5
ok: [localhost] => {
    "msg": "<built-in method update of dict object at 0x7fab6c288f40>"
}

TASK [os_software : debug] *****************************************************************************************************************************
task path: ./roles/os_software/tasks/apt/main.yml:8
ok: [localhost] => {
    "msg": [
        {
            "name": "python3-apt"
        },
        {
            "name": "python3-dev"
        },
        {
            "name": "python3-pip"
        }
    ]
}
```
### Question:

Why is this? onetime i can call without problems. On the other Hand it results in a uncaled Object. Any edits like create a list under Software results in other errors (like they shoud).

### Workaround/ Best Practice:

On [RedHat](https://www.redhat.com/sysadmin/ansible-lists-dictionaries-yaml) has a realy good explanaition with many diffrent casses by processing lists and dicts with Ansible.
Like they said it works with the following main.yml file:
```
    - debug:
        msg: "{{ software }}"

    - debug:
        msg: "{{ software['update'] }}"

    - debug:
        msg: "{{ software['apt'] }}"
```
