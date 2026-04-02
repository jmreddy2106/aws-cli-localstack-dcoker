# Create an S3 bucket, enable versioning, upload the same file multiple times, and verify version history.

## Concepts
 - S3 stores objects (files) in buckets.
 - Versioning preserves every overwrite/delete as a new version.
 - Each version has a unique VersionId.

 ## Steps
 - Create the S3 Bucket
```bash
    awslocal s3api create-bucket --bucket my-versioned-bucket --region us-east-1

    Expected output: { "Location": "/my-versioned-bucket" }
```

- Enable Versioning
```bash
    awslocal s3api put-bucket-versioning --bucket my-versioned-bucket --versioning-configuration Status=Enabled
```

- Verify Versioning is Enabled
```bash
    awslocal s3api get-bucket-versioning --bucket my-versioned-bucket

    Expected Output: { "Status": "Enabled" }
```
- Create a Sample File and Upload Multiple Versions
```bash
# Version 1
    echo "Hello World - Version 1" > sample.txt
    awslocal s3 cp sample.txt s3://my-versioned-bucket/sample.txt

# Version 2
    echo "Hello World - Version 2" > sample.txt
    awslocal s3 cp sample.txt s3://my-versioned-bucket/sample.txt
# Version 3
    echo "Hello World - Version 3" > sample.txt
    awslocal s3 cp sample.txt s3://my-versioned-bucket/sample.txt
```

- List All Versions
```bash
    awslocal s3api list-object-versions --bucket my-versioned-bucket --prefix sample.txt
```
You will see 3 versions each with a unique VersionId.

- Retrieve a Specific Version
```bash
# Copy the VersionId from Step 5 output
    awslocal s3api get-object --bucket my-versioned-bucket --key sample.txt --version-id <VersionId> downloaded_v1.txt

    cat downloaded_v1.txt
```

- Delete a Specific Version
```bash
    awslocal s3api delete-object --bucket my-versioned-bucket --key sample.txt --version-id <VersionId>
```


