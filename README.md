# guardduty
参数设置
```
bucketname=gdti
region=us-east-1
filenam=threatlist.txt
ThreatSet=xthreatbookcn
```
CLI命令
```
aws s3api create-bucket \
    --bucket $bucketname \
    --region $region
    
aws s3 cp $filename s3://$bucketname/ --region=$region
aws guardduty create-threat-intel-set \
    --detector-id $(aws guardduty list-detectors --output text --query 'DetectorIds' --region=$region)  \
    --name $ThreatSet \
    --format TXT \
    --location s3://$bucketname/$filenam\
    --activate --region=$region
```
