=================
 PUBLIC
=================
sam build

sam package \
  --template-file template.yaml \
  --output-template-file packaged.yaml \
  --s3-bucket sam-app-demo-local

sam deploy \
  --template-file packaged.yaml \
  --stack-name sam-app-demo-local-stack \
  --capabilities CAPABILITY_IAM \
  --region ap-northeast-1

curl https://mb4bisn1bl.execute-api.ap-northeast-1.amazonaws.com/Prod/hello


=================
 PRIVATE
=================
vpc-07a551389a04caacb
10.5.5.0/24
subnet-0a0d222d65796d690
subnet-066ce9fce3a64b3ce

sam build

sam package \
  --template-file template.yaml \
  --output-template-file packaged.yaml \
  --s3-bucket sam-app-demo-local

sam deploy \
  --template-file packaged.yaml \
  --stack-name sam-app-demo-local-stack \
  --capabilities CAPABILITY_IAM CAPABILITY_NAMED_IAM \
  --region ap-northeast-1

=================
 SessionManager
=================
1. IAMロールの作成:
    AWSマネジメントコンソールでIAMサービスに移動します。
    「ロール」を選択し、「ロールの作成」をクリックします。
    ユースケースとして「EC2」を選択し、「次のステップ：許可」をクリックします。
    「ポリシーをアタッチ」で AmazonSSMManagedInstanceCore を選択し、「次のステップ：確認」をクリックします。
    ロールに名前を付けて（例： SSMAccessRole ）、ロールを作成します。
2. EC2インスタンスにロールをアタッチ:
    EC2サービスに移動し、インスタンスを選択します。
    「インスタンスの詳細」タブで「IAMロールの変更」をクリックします。
    作成したIAMロール（例： SSMAccessRole ）を選択し、「更新」をクリックします。

=================
 SSH
=================
ssh -i ~/.aws/sam-test-key.pem ec2-user@ec2-18-183-83-160.ap-northeast-1.compute.amazonaws.com
scp -i ~/.aws/sam-test-key.pem ~/.aws/sam-test-key.pem ec2-user@ec2-18-183-83-160.ap-northeast-1.compute.amazonaws.com:/home/ec2-user/
ssh -i sam-test-key.pem ec2-user@ip-10-5-5-125.ap-northeast-1.compute.internal

=================
 CURL
=================
curl https://exro9eq8f3.execute-api.ap-northeast-1.amazonaws.com/Stage/private-api-endpoint/private-api
curl -X POST "https://exro9eq8f3.execute-api.ap-northeast-1.amazonaws.com/Stage/private-api-endpoint"
curl https://exro9eq8f3.execute-api.ap-northeast-1.amazonaws.com/dev/private-api-endpoint/private-api
curl -X POST "https://exro9eq8f3.execute-api.ap-northeast-1.amazonaws.com/dev/private-api-endpoint"

curl https://exro9eq8f3.execute-api.ap-northeast-1.amazonaws.com/test/private-api-endpoint/private-api


=================
 参考
=================
AWS SAMで「Stage」ステージが作られるバグを回避する
https://medium.com/veltra-engineering/avoid-aws-sam-stage-stage-45f7331b7b5d
https://dev.classmethod.jp/articles/aws-sam-delete-deploy-unused-stage/

