# AWS Connect Solution For Alerts

# Need for this solution?
The purpose of this solution is to provide the way to get notified via automated calls on event of any failure. One may miss the text messages or slack messages during failure events. This solution calls the three provided contacts. For example on event of failure first person will be called, incase he cannot fix the issue or may be busy he can transfer the call to second person by choosing the suitable IVR options and so on. 

# How this works?
Cloudwatch alarm is generated and notifies to the sns topic created by this template and makes the call to the team's person.

# How to setup the solution?
Step 1:
Create the amazon connect instance by following the aws proivded doc: https://docs.aws.amazon.com/connect/latest/adminguide/gettingstarted.html

Step 2:
Navigate to https://NAME-YOU-PROVIDED.awsapps.com/connect/contact-flows and import the connect-1 from the ConnectFlow folder, name this as connect-1 and press save. Please note the contact-flow id copy it from URL bar. Example url ends with contact-flow/25df8ad7-a765-4eebf-8200-82a92b3b342dc you need to copy numeric part "5df8ad7-a765-4eebf-8200-82a92b3b342dc"

Step 3:
Navigate to https://NAME-YOU-PROVIDED.awsapps.com/connect/contact-flows and import the connect-2 from the ConnectFlow folder, name this as connect-2 and press save. Please note the contact-flow id copy it from URL bar. Example url ends with contact-flow/25df8ad7-a765-4eebf-8200-82a92b3b342dc you need to copy numeric part "5df8ad7-a765-4eebf-8200-82a92b3b342dc"

Step 4:
Navigate to https://NAME-YOU-PROVIDED.awsapps.com/connect/contact-flows and import the connect-3 from the ConnectFlow folder, name this as connect-3 and press save. Please note the contact-flow id copy it from URL bar. Example url ends with contact-flow/25df8ad7-a765-4eebf-8200-82a92b3b342dc you need to copy numeric part "5df8ad7-a765-4eebf-8200-82a92b3b342dc"

Step 5:
Please note the instance id from the same url bar where the contact-flow is copied. Example instance/7cdce286-6fbf-4d62-bd91-b2fbb4e730fe/ copy the numeric part example 7cdce286-6fbf-4d42-bd31-b2fbb4e730fd.

Step 6:
Navigate to https://NAME-YOU-PROVIDED.awsapps.com/connect/numbers and claim a number and note the number as well.

Step 7:
Launch Solution Stack
[![Launch Stack](https://cdn.rawgit.com/buildkite/cloudformation-launch-stack-button-svg/master/launch-stack.svg)](https://console.aws.amazon.com/cloudformation/home#/stacks/new?stackName=buildkite&templateURL=https://s3.amazonaws.com/aws-connect-sf-poc/main.yaml)

###### Solution Architecture 
![Optional Text](https://github.com/sourcefuse/aws-connect/blob/master/connect-arch.png)

###### Connect Flow Diagram
![Optional Text](https://github.com/sourcefuse/aws-connect/blob/master/connect.png)


