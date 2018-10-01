# ansible-rhel7-disa-stig-role

This project reflects the USGS STIG for RHEL 7 (and similar) systems. The
STIG is checked and possibly implemented via Ansible. The playbook was
originally generated using the following commands on an RHEL 7 system:

```
$ yum install -y scap-security-guide
$ oscap xccdf generate fix \
  --fix-type ansible \
  --profile xccdf_org.ssgproject.content_profile_stig-rhel7-disa \
  --output stig-rhel7-role.yml \
  /usr/share/xml/scap/ssg/content/ssg-rhel7-ds.xml
```

The playbook was then modified to suite the USGS environment. The playbook can
be run on a system by cloning this repository, navigating to the
`ansible-rhel7-disa-stig-role` directory, and running the following
command:

```
$ ansible-playbook -i "localhost," -c local --check stig-rhel7-role.yml
```

Optionally omit the `--check` switch to have Ansible attempt to apply the
necessary fixes.