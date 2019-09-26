Copy Glance image playbook
=========

This playbook copies Glance image from source Glance domain to
destination Glance domain. As of now, both of the Glance domains need to
be registered in the same oVirt engine. The simplified flow looks like 
this:

- Image from source Glance domain is imported as a template to oVirt engine
- Disk of that oVirt template is exported as image to destination Glance domain
- The intermediary template (along with its disk) are deleted from oVirt engine

You need to provide some variables to run the playbook successfully. Their list is in the `vars` section of the play and I believe they are pretty self-explanatory. They are separated into three parts:

- The first part may contain sensitive data, therefore you might want to encrypt those variables with ansible-vault
- The second part holds information about your oVirt engine environment 
- You most probably won't need to edit the third part - those are variables pertaining to creation of intermediary template in oVirt engine

Run the playbook for example like this:
```bash
$ ansible-playbook -e@glance_vars.yml -e@sensitive_vars.yml copy_glance_image.yml --ask-vault-pass
```

Requirements
------------

You need to have the following pip packages installed:

- openstacksdk
- ovirt-engine-sdk-python
