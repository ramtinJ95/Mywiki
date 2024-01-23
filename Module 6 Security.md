# Security

__AWS Artifact__ is a service that provides on-demand access to aws security and
complience reports and sleect online agreements. Aws artifact consists of two
main sections;
- __AWS Artifact Agreements__ is used by you as a user of AWS when you need to
  sign an agreement regarding your use of certain information throughout the aws
  services.
- __AWS Artifact Reports__, suppose a dev is building an app and needs more info
  about their responsability for complyting wiht vertain regulatory standards.
  Reports provide compliance reports from third party auditors. These auditors
  have tested and verified that aws is compliant with a variety of
  global,regional and industry specific security standards and regulations.
  
  In the Customer Complience Center you can read customer compliance stories to
  discover how companies in regulated industries have solved various compliance,
  governance and audit challenges. You can also access compliance whitepapers
  and documentation on topics such as; AWS answers to key complience questions,
  an overview of aws risk and compliance and auditing security checklist.
  
  __AWS Shield__ is the service thta protects applications against DDoS attacks.
  Shield comes with two levels of protection:
  - __Standard__, this tier automatically protects all aws cutomers against the
    most common and frequent occuring types of DDoS attack to no cost
  - __Advanced__, is a paid service that provides detailed attack diagnostics
    and the ability to detect and mitigate sophisticated DDoS attacks. It also
    integrates with other Services such as Amazon cloudfront, route 53 and
    elastic load balancing. Additonally, you can integrate aws shield with aws
    waf by writing custom rules to mitigate complex DDoS attacks.
    
__AWS KMS__ enables you to perform encryption operations through the use of
cryptographic keys. You can use the KMS to create, manage and use the crypto
keys. You van also control the use of keys acceos a wide range of services and
in your apps with KMS, you can choose specific levels of access control that you
need for your keys. For example, you can specify which IAM users and roles are
able to manage keys. Alternatively, you can temporarily disable keys so that
they are no longer in use by anyone. Your jeys never leave KMS and you are
always in control of them.

__AWS WAF__ is a web application firewall that lets you monitor network requests
that come in your web applicatons. WAF works together with CloudFront and an
applicaton load balancer. It does this by using ACL to protect your aws
resources.

__Amazon Inspector__ help to improve the security and compliance of applicatons
by running automated security assesments. It checks applications for security
vulnaerabilities and deviations from security best practises, such as open
access to EC2 instances and installations of vulnerable software versions.
Inspector then provides you with a list of security findings. Aws does not
gurantee that following the provided recommendations resolves every potential
security issue.

__Amazon GuardDuty__ is a service that provides intelligent threat assesment for
your aws resources. It monitors the network and account activity continously
withing your aws environment. There is no need to deploy any resources to use
GuardDuty. If threats are discoverd you can find the list and recommended
remedies in the amazon managament consol. You can also configure aws lambda
functuins to take remedition steps automatically in response to GuardDuty's
findings. 

one key difference between WAF and Shield is that Shield operates at a lower
level in the network stack and can thus protect against DDoS attack. While WAF
operates at a high level in the stack and thus it can take action based on
specific contents od web traffic and requests.
