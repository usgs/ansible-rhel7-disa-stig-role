> This project has been archived to internal resources as of 2019-03-18.

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
be run on a system by running the following command:

```
$ $ ansible-pull \
  -U https://github.com/usgs/ansible-rhel7-disa-stig-role.git \
  -i "localhost," \
  --check \
  stig-rhel7-role.yml
```

Optionally omit the `--check` switch to have Ansible attempt to apply the
necessary fixes.

## Installing Ansible

```
$ rpm -ivh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
$ yum install -y ansible git
```
