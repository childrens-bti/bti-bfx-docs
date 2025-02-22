# Access to Resources and Tools

## GitHub

We operate two GitHub organizations, [the Rokita Lab](https://github.com/rokitalab) and [BTI Bioinformatics Core](https://github.com/childrens-bti). All Rokta Lab and BTI Bioinformatics Core staff should be added to both.

## High Performance Cluster (HPC)

### Requesting access

While on VPN, fill out [this](https://criowiki.cnmc.org/doku.php?id=hpc:access) form for HPC access.

### HPC basics 

The HPC Wiki can be found [here](https://criowiki.cnmc.org/doku.php?id=hpc:start). 

- To view available modules, use `module avail`.
- To load modules, use module load xxx
- To mount L drive folders (e.g. to mount the L Drive folder `CancerImmunology-BTI`), follow the instructions below, changing the group to the group to which you belong.

```bash
#!/bin/bash

# Add this file under $HOME/.bashrc.d/ with permission '0640'

FOLDER=$HOME/CancerImmunology-BTI
CIFS="//cnmc.org/CRI_LAB1/CancerImmunology-BTI"
GROUP="rokitagrp"

# There settings are generally fine
USER=$(whoami)
FILE_MODE='0750'
DIR_MODE='0750'


case $(hostname) in
    pphpcln*|pphpcdtn* )

    if [ ! -d $FOLDER ]; then
        mkdir -p $FOLDER
    fi

    if ! mountpoint -q $FOLDER
    then

        echo $FOLDER is not mounted
        echo Mounting it...

        sudo /usr/sbin/mount.cifs -o username=${USER},domain=cnmc.org,uid=${USER},gid=${GROUP},dir_mode=${DIR_MODE},file_mode=${FILE_MODE} $CIFS $FOLDER

    fi

esac
```

After sourcing this file, you should be able to see the folder in `/home/USER/CancerImmunology-BTI`.

## Amazon Web Services (AWS)

For information about our account, please see pinned file in Slack.

### Requesting access

1. First, obtain email approval from Dr. Jo Lynne Rokita for access to the BTI Bioinformatics AWS account. 
2. Open a Service Catalog item in [Service Now](https://childrensnational.service-now.com/esc?id=ec_pro_dashboard) using the "Add user to existing Access Group for AWS" template.

- AWS account name and number = `<see slack for account number>`
- Request ReadOnly access

### Accessing AWS through the console

Once access is granted, you should be able to access our account using CNH SSO credentials using [this URL](https://d-9067576cea.awsapps.com/start/). You will have read access to S3 buckets and EC2 Service Catalog launch permissions.

## CAVATICA

If you do not already have an account, you can generate one using your eCommons ID [here](https://cavatica.sbgenomics.com/). If you do not have an eCommons ID, please work with Dr. Rokita to get one.


## Self-service password reset

On occasion, your password may be reset without warning (!). To reset it, go to [this url](https://cnh.identitynow.com/r/default/reset-password) and follow the instructions.

## Box

We use Box to store various documents for grants, manuscripts, presentations, and collaborator files. Open a Service Catalog item in [Service Now](https://childrensnational.service-now.com/esc?id=ec_pro_dashboard) and request access to Box for Children's National.

## Google Drive

We favor Google Drive over OneDrive for collaborative manuscript writing and collaborative documentation. Currently, Google Drive is sometimes (or always?) blocked on PCs, but to date, it is available on Apple devices. 

## Paperpile

We have paperpile licenses for individuals actively writing manuscripts on Google Drive needing to insert references. Please ask Dr. Rokita for a license.

