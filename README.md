# aws-sdk-layers 
By default the NodeJS lambda environment does not have a current aws-sdk installed but sadly an outdated version, so here is a snippet to create and include a layer

## Cloudformation

Create NodeJS Lamnda Layer:
```
LatestAWKSDK:
    Type: AWS::Lambda::LayerVersion
    Properties:
      CompatibleRuntimes:
        - nodejs12.x
        - nodejs10.x
      Content: 
        S3Bucket: aws-sdk-layers
        S3Key: package.zip
      LayerName: LatestAWKSDK
```

Integration:
```
MayLambdaFuction:
    Type: AWS::Serverless::Function
    Properties:
      Handler: index.handler
      Runtime: nodejs14.x
      Layers: 
        - !Ref LatestAWKSDK
```
