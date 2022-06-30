# guardduty
参数设置
```
bucketregion=us-east-1
bucketname=gdti
region=us-east-1
filenam=threatlist.txt
ThreatSet=xthreatbookcn
regions=($(aws ec2 describe-regions --query 'Regions[*].RegionName' --output text))
```
CLI命令
```
aws s3api create-bucket \
    --bucket $bucketname \
    --region $bucketregion
aws s3 cp $filename s3://$bucketname/ --region=$bucketregion
```
在所有regions部署TI

```
for region in $regions; do
aws guardduty create-threat-intel-set \
    --detector-id $(aws guardduty list-detectors --output text --query 'DetectorIds' --region=$region)  \
    --name $ThreatSet \
    --format TXT \
    --location s3://$bucketname/$filenam\
    --activate --region=$region
echo $region
done
```
告警展示:
![sample](/FindingSample.png)
