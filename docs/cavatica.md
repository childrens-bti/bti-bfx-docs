# CAVATICA Computing

CAVATICA is a platform which enables users to run AWS compute jobs through Common Workflow Language (CWL). As such, we have to pay for analyses run on CAVATICA _and_ storage of data on CAVATICA which is not mounted to any of our AWS S3 buckets. Keeping this in mind, we will discuss as a team what can be run when and with what money.

We will generally use CAVATICA to:

1. Run upstream processing workflows on raw data files, for example, those created through the Kids First Data Resource Center (KF DRC) at CHOP
2. Benchmark and implement new workflows specific to the needs of the BTI, for example, CITE-Seq, miRNA-Seq, pangenome analyses, etc.
3. Small-scale merges/quick analyses of many data files to avoid downloads, such as through Data Studio.

## How to mount an AWS volume in CAVATICA

In order to mount an AWS volume, you need to have access keys to our AWS account. We will not give these out to everyone, so generally, Alex Sickler and Jo Lynne Rokita will be the ones with keys for mounting. Lordley Okarter, who is the AWS account admin, is the only one who can create these.

Once you have keys:

1. Go to Data —> Volumes
2. Follow the instructions for the bucket you would like to mount
3. Copy the IAM policy, save it as a JSON file, and add it via PR to the [BTI bucket policy repository](https://github.com/childrens-bti/bti-aws-bucket-policies). Then, send this JSON file to Lordley Okarter (cc Jo Lynne), as he is currently the only person who can add these to the IAM policy for our AWS account. Once Lordley confirms this was added, you can proceed.
4. Add your access keys.
5. For FIPS, use `s3-fips.us-east-1.amazonaws.com`
6. For encryption, use `default 256`.

Note: we usually will mount these as read/write if we desire to export data back to the bucket.

Additional documentation on mounting volumes inside of CAVATICA can be found [here](https://docs.cavatica.org/docs/volumes).
