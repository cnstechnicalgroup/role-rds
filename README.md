Role: cns.ec2
========

This role initializes RDS instances. Use count to limit exact instance count (grouped by Name tag).

Requirements
------------

Nothing, it runs out of the box.

Role Variables
--------------

In the current version, you can specify the following variables:

| Name               | Default |                                                        |
|--------------------|---------|--------------------------------------------------------|
| site_prefix        |   ---   | Prefix to use for AWS object naming.                   |
| keypair            |   ---   | AWS registered SSH keypair to install on RDS instance  |
| region             |   ---   | Region in which the resource exists.                   |
| zone               |   ---   | Availability zone in which the resource exists.        |
| name               |   ---   | Name of RDS instance.                                  |
| owner              |   ---   | RDS instance owner for billing.                        |
| instance           |   ---   | Object containing instance details (see example).      |
| dev_db_sg          |   ---   | Optional Security Group name for dev RDS instances.    |

Dependencies
------------

This package has no dependencies.

License
-------

GPLv2

Author Information
------------------

Created by Sam Morrison [@samcns](https://www.twitter.com/samcns)

Examples
--------

```yaml
---
- name: cns.rds role test
  hosts: all
  roles:
    - cns.rds
```

```yaml
---
# Dict containing RDS instance configuration
instance_rds_prestashop:
  rds:
    # Prefix override
    prefix: "{{ site_prefix }}"
    # RDS instance app (prestashop, wordpress, redmine, etc.)
    app: "wordpress"
    # Environment: dev, test, stage, or prod
    mode: "dev"
    # DB Name
    db_name: "wordpress"
    # DB username
    db_username: "wordpress"
    # DB password
    db_password: "nobody can hack me"
    # Is this a multi-zone instance?
    multizone: no
    # Region override
    region: "{{ region }}"
    # RDS instance type
    instance_type: "db.t2.micro"
    # Total number of instances for this type
    count: 1
```
