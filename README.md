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
