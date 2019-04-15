//create bucket
aws s3 mb s3://utkal-bucket-1234

//list buckets
aws s3 ls

//list objects within bucket
aws s3 ls s3://utkal-bucket-1234

//delete bucket
aws s3 rb s3://utkal-bucket-1234

//force delete
aws s3 rb s3://utkal-bucket-1234 --force

//upload local file with storage class option
aws s3 cp local-file.txt s3://utkal-bucket-1234 --storage-class REDUCED_REDUNDANCY

//sync everything from local folder to s3
aws s3 sync . s3://utkal-bucket-1234

