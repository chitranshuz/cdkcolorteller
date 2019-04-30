# ColorTeller - AppMesh, X-Ray + Fargate Demo using AWS CDK

colorteller, appmesh envoy Docker images are hosted on dockerhub for now.

## Quick start (in AWS Cloud9 or anywhere)

```
nvm install 8.14.0
nvm alias default v8.14.0
npm i -g aws-cdk
npm install
npm run build
cdk deploy
```
Once fully deployed, go to the newly created ALB and access its ``/color`` endpoint multiple times. the json output should rotate the 3 colors evenly.
eg:
http://farga-exter-yt5qsba6l5n1-1671653105.ap-southeast-1.elb.amazonaws.com/color

Refer to this blog post for more info:
https://medium.com/containers-on-aws/aws-app-mesh-walkthrough-deploy-the-color-app-on-amazon-ecs-de3452846e9d


## Useful commands

 * `npm run build`   compile typescript to js
 * `npm run watch`   watch for changes and compile
 * `cdk deploy`      deploy this stack to your default AWS account/region
 * `cdk diff`        compare deployed stack with current state
 * `cdk synth`       emits the synthesized CloudFormation template


## AWS X-Ray
In AWS Xray console, choose “Create group”, name the group “color”, and enter the expression that filters all the ``/color`` requests.

```
(service("colormesh/colorgateway-vn")) AND http.url ENDSWITH "/color"
```

![AWS Xray diagram](img/xray.png)