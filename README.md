# ansible-rhel7-disa-stig-role

This project reflects the USGS STIG for RHEL 7 (and similar) systems.

## Getting Started

To run this playbook, log in to the RHEL 7 (or similar) system on which the
STIG is to be applied. Ansible is required on this system (see below). The
system's current compliance can be checked with the `--check` switch
(see below). The system can be manually configured to meet compliance or
Ansible may be run without the `--check` switch to apply the necessary changes.

This is tested and known to work with basic RHEL 7 (or similar) systems, but
may produce unexpected results with custom configurations.

### Install Ansible

```
$ rpm -ivh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
$ yum install -y ansible git
```

### Check Compliance

The playbook can be run with the `--check` switch to examine the current state
of the system The playbook can be run on a system by running the following command:

```
$ ansible-pull \
  -U https://github.com/usgs/ansible-rhel7-disa-stig-role.git \
  -i "localhost," \
  --check \
  stig-rhel7-role.yml
```

### Automatically Apply STIG (Optional)

The STIG can be automatically applied to bring your system into compliance by
ommitting the `--check` switch from the previous command. For example:

```
$ ansible-pull \
  -U https://github.com/usgs/ansible-rhel7-disa-stig-role.git \
  -i "localhost," \
  stig-rhel7-role.yml
```

If you choose not to automatically apply the STIG settings, you must manually
apply them yourself. You can repeatedly `Check Compliance` using the command
in the section above in order to verify your system is in compliance.


### Provenance

The playbook was originally generated using the following commands on an
RHEL 7 system:

```
$ yum install -y scap-security-guide
$ oscap xccdf generate fix \
  --fix-type ansible \
  --profile xccdf_org.ssgproject.content_profile_stig-rhel7-disa \
  --output stig-rhel7-role.yml \
  /usr/share/xml/scap/ssg/content/ssg-rhel7-ds.xml
```

The playbook was then modified to suite the USGS environment.
