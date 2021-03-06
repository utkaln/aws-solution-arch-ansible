# Exercise 2.1, 2.2 done using CLI
# Created bucket
aws s3 mb s3://utkal-aws-certi

# List of files
aws s3 ls
  
# Copied image to S3 bucket
aws s3 cp sample-image.png s3://utkal-aws-certi/ --storage-class REDUCED_REDUNDANCY

# Evidence: 2018-10-29 15:38:09     113489 sample-image.png

# Make the object public
aws s3 cp sample-image.png s3://utkal-aws-certi/ --storage-class REDUCED_REDUNDANCY --acl public-read
# upload: ./sample-image.png to s3://utkal-aws-certi/sample-image.png

# Rename file that was uploaded
aws s3 mv s3://utkal-aws-certi/sample-image.png s3://utkal-aws-certi/sample-image1.png
# move: s3://utkal-aws-certi/sample-image.png to s3://utkal-aws-certi/sample-image1.png
# Observe that the ACL property went off without ACL written
# Fixing the public read property

aws s3 mv s3://utkal-aws-certi/sample-image1.png s3://utkal-aws-certi/sample-image2.png --storage-class REDUCED_REDUNDANCY --acl public-read

# Exercise 2.3
# Enable versioning
aws s3api put-bucket-versioning --bucket utkal-aws-certi --versioning-configuration Status=Enabled

# Add a version 1 of the file
aws s3 cp sampletext1.txt s3://utkal-aws-certi/ --storage-class REDUCED_REDUNDANCY --acl public-read

# modify the file and upload again then check version
aws s3api list-object-versions --bucket utkal-aws-certi --prefix sampletext1.txt
# Output
  {
    "Versions": [
        {
            "ETag": "\"51be4b005a7a72bfad69f2e0c39587f8\"",
            "Size": 15,
            "StorageClass": "REDUCED_REDUNDANCY",
            "Key": "sampletext1.txt",
            "VersionId": "pjQKIC8y8_dEd8ExLFR3Jmg.RYCYBWX2",
            "IsLatest": true,
            "LastModified": "2018-10-29T20:11:52.000Z",
            "Owner": {
                "DisplayName": "unayak",
                "ID": "da8a300f609223c2ae2ae382a9fe0d9ad35b625d1aafbd8b42159a42818218b2"
            }
        },
        {
            "ETag": "\"b954b7ef3a92a2af91f9dd765073f205\"",
            "Size": 16,
            "StorageClass": "REDUCED_REDUNDANCY",
            "Key": "sampletext1.txt",
            "VersionId": "O6CSPhv0gE3MUBOWrbw_fNp0oq2L66XV",
            "IsLatest": false,
            "LastModified": "2018-10-29T20:10:43.000Z",
            "Owner": {
                "DisplayName": "unayak",
                "ID": "da8a300f609223c2ae2ae382a9fe0d9ad35b625d1aafbd8b42159a42818218b2"
            }
        }
    ]
  }
 
# Exercise 2.4
# Delete object from bucket with version enabled and restore
utkalnayak$ aws s3api delete-object --bucket utkal-aws-certi --key sampletext1.txt

# Output
    {
        "DeleteMarker": true,
        "VersionId": "cGtui5h_f1EuMfcL5fWEG6nCSoo55x6y"
    }

# Check status of the file version
aws s3api list-object-versions --bucket utkal-aws-certi --prefix sampletext1.txt

# Output
    {
    "Versions": [
        {
            "ETag": "\"51be4b005a7a72bfad69f2e0c39587f8\"",
            "Size": 15,
            "StorageClass": "REDUCED_REDUNDANCY",
            "Key": "sampletext1.txt",
            "VersionId": "pjQKIC8y8_dEd8ExLFR3Jmg.RYCYBWX2",
            "IsLatest": false,
            "LastModified": "2018-10-29T20:11:52.000Z",
            "Owner": {
                "DisplayName": "unayak",
                "ID": "da8a300f609223c2ae2ae382a9fe0d9ad35b625d1aafbd8b42159a42818218b2"
            }
        },
        {
            "ETag": "\"b954b7ef3a92a2af91f9dd765073f205\"",
            "Size": 16,
            "StorageClass": "REDUCED_REDUNDANCY",
            "Key": "sampletext1.txt",
            "VersionId": "O6CSPhv0gE3MUBOWrbw_fNp0oq2L66XV",
            "IsLatest": false,
            "LastModified": "2018-10-29T20:10:43.000Z",
            "Owner": {
                "DisplayName": "unayak",
                "ID": "da8a300f609223c2ae2ae382a9fe0d9ad35b625d1aafbd8b42159a42818218b2"
            }
        }
    ],
    "DeleteMarkers": [
        {
            "Owner": {
                "DisplayName": "unayak",
                "ID": "da8a300f609223c2ae2ae382a9fe0d9ad35b625d1aafbd8b42159a42818218b2"
            },
            "Key": "sampletext1.txt",
            "VersionId": "cGtui5h_f1EuMfcL5fWEG6nCSoo55x6y",
            "IsLatest": true,
            "LastModified": "2018-10-30T00:47:56.000Z"
        }
    ]
  }

# Upload the same file again
aws s3 cp sampletext1.txt s3://utkal-aws-certi/ --storage-class REDUCED_REDUNDANCY --acl public-read

# Check status of the file version
aws s3api list-object-versions --bucket utkal-aws-certi --prefix sampletext1.txt

# Output
    {
    "Versions": [
        {
            "ETag": "\"51be4b005a7a72bfad69f2e0c39587f8\"",
            "Size": 15,
            "StorageClass": "REDUCED_REDUNDANCY",
            "Key": "sampletext1.txt",
            "VersionId": "9jY11iWR63Fblv1p_hi.7WZRibv9f5JQ",
            "IsLatest": true,
            "LastModified": "2018-10-30T01:05:24.000Z",
            "Owner": {
                "DisplayName": "unayak",
                "ID": "da8a300f609223c2ae2ae382a9fe0d9ad35b625d1aafbd8b42159a42818218b2"
            }
        },
        {
            "ETag": "\"51be4b005a7a72bfad69f2e0c39587f8\"",
            "Size": 15,
            "StorageClass": "REDUCED_REDUNDANCY",
            "Key": "sampletext1.txt",
            "VersionId": "pjQKIC8y8_dEd8ExLFR3Jmg.RYCYBWX2",
            "IsLatest": false,
            "LastModified": "2018-10-29T20:11:52.000Z",
            "Owner": {
                "DisplayName": "unayak",
                "ID": "da8a300f609223c2ae2ae382a9fe0d9ad35b625d1aafbd8b42159a42818218b2"
            }
        },
        {
            "ETag": "\"b954b7ef3a92a2af91f9dd765073f205\"",
            "Size": 16,
            "StorageClass": "REDUCED_REDUNDANCY",
            "Key": "sampletext1.txt",
            "VersionId": "O6CSPhv0gE3MUBOWrbw_fNp0oq2L66XV",
            "IsLatest": false,
            "LastModified": "2018-10-29T20:10:43.000Z",
            "Owner": {
                "DisplayName": "unayak",
                "ID": "da8a300f609223c2ae2ae382a9fe0d9ad35b625d1aafbd8b42159a42818218b2"
            }
        }
    ],
    "DeleteMarkers": [
        {
            "Owner": {
                "DisplayName": "unayak",
                "ID": "da8a300f609223c2ae2ae382a9fe0d9ad35b625d1aafbd8b42159a42818218b2"
            },
            "Key": "sampletext1.txt",
            "VersionId": "cGtui5h_f1EuMfcL5fWEG6nCSoo55x6y",
            "IsLatest": false,
            "LastModified": "2018-10-30T00:47:56.000Z"
        }
    ]
}


# Exercise 2.5
# Check life cycle config
aws s3api get-bucket-lifecycle-configuration --bucket utkal-aws-certi

# Output : An error occurred (NoSuchLifecycleConfiguration) when calling the GetBucketLifecycleConfiguration operation: The lifecycle configuration does not exist


aws s3api put-bucket-lifecycle-configuration --bucket utkal-aws-certi --lifecycle-configuration  file://lifecycle.json
# Output : [BLANK]

# Exercise 2.6
# Static website hosting
aws s3api put-bucket-website --bucket utkal-aws-certi --website-configuration file://website.json
aws s3 cp index.html s3://utkal-aws-certi/ --storage-class REDUCED_REDUNDANCY --acl public-read
aws s3 cp error.html s3://utkal-aws-certi/ --storage-class REDUCED_REDUNDANCY --acl public-read

aws s3api get-bucket-website --bucket utkal-aws-certi

# Endpoint : http://utkal-aws-certi.s3-website-us-east-1.amazonaws.com








