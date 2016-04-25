The code is serving as a working example for interacting with the Icinga2 API with Ansible.
It is not advisable to open any ports to the public internet without enforcing safe authentication mechanisms.

The code was tested on:

```bash
$ ansible --version
ansible 2.1.0 (devel cfe99b991f) last updated 2016/04/18 21:23:33 (GMT +200)
  lib/ansible/modules/core: (detached HEAD 5409ed1b28) last updated 2016/04/18 21:23:52 (GMT +200)
  lib/ansible/modules/extras: (detached HEAD 3afe117730) last updated 2016/04/18 21:23:52 (GMT +200)
  config file = /Users/danvaida/work/github/Ansible-Berlin-Meetup/ansible-icinga2-api/ansible.cfg
  configured module search path = Default w/o overrides

$ VBoxManage --version
5.0.14r105127
```
It is expected to work with previous versions as well (only minor versions).

Here are some useful snippets throughout the example:

```bash
$ vagrant up && ansible-playbook icinga.yml
$ ansible-playbook icinga.yml --tags icinga2-api --extra-vars 'icinga2_api_method=POST'

$ vagrant ssh icinga2a -c 'sudo icinga2 object list --type hostgroup --name databases'
$ vagrant ssh icinga2b -c 'sudo icinga2 object list --type hostgroup --name webservers'

$ vagrant ssh icinga2a -c 'sudo icinga2 object list --type service --name diggy'
$ vagrant ssh icinga2b -c 'sudo icinga2 object list --type service --name flipper'

$ curl -k -s -u icinga2a:HereGoesSomething -X GET -H 'Accept: application/json' 'https://10.10.10.10:5665/v1/objects/services/icinga2a!diggy' | python -m json.tool

$ curl -k -s -u icinga2b:HereGoesNothing -X GET -H 'Accept: application/json' 'https://10.10.10.11:5665/v1/objects/services/icinga2b!flipper' | python -m json.tool
```

Thanks for public hosts with open ports, found on:
* http://www.ensembl.org/info/data/mysql.html
* http://shells.red-pill.eu
