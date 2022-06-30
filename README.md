# guardduty
参数设置
```
bucketname=gdti
region=us-east-1
filenam=threatlist.txt
```
CLI命令
```
aws s3api create-bucket \
    --bucket $bucketname \
    --region $region
    
aws s3 cp $filename s3://$bucketname/ --region=$region
```
