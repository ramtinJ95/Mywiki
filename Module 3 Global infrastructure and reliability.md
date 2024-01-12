# Global infrastructure and reliablility

__Edge locations__; Edge locations is a site that Amazon Cloudfront uses to
store cached copies of your content closer to your customers for faster
delivery.

__Provision of AWS resources__; With AWS Elastic Beanstalk you provide code and
configuration settings and elastic beanstalk deploys the resources necessary to
perform the following tasks;
- Adjust capacity
- Load balancing
- Automatic scaling
- Application health monitoring

__AWS CloudFormation__; you can treat your infra as code. Cloudformation
provisions your resourves in a safe, repeatable manner enabling you to
frequently build your infrastrucuture and applications without having to perform
manual actions. It determines the right operations to perform when managing your
stack and rolls back changes automatically if it detects errors.

__CloudFront__; should not be confused with cloudformation. CloudFront id a
global content delivery service.

__AWS Outposts__; Extends AWS infrastrucutre and service to different locations
including your on-premises data center.
