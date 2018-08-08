# Build you own Pager Duty Alternative with AWS Connect and Polly

# Need for this solution?
SourceFuse is an AWS certified advanced partner and provides managed services solutions to enterpirse clients in the US and the UK. A part of the managed services is a 99.99% uptime SLA. We need  to ensure that our systems are always up and running, however, we know things do happen in production - User errors, uncaught exceptions, Slow queiries, CPU over-utilization. We need to respond to these kinds of incidents immediately. Since we are a geographically dispersed team, we are able to provide 24x7 support but we cannot only rely on Slack and Email for alerts. Our DevOps team needed a solution to alert them in real time about production incidents, so we came up with a quick and effective way to have a call flow using AWS Cloudwatch alarms as triggers and Amazon Connect + Polly to make phone calls to our support engineers in case of an incident.  


# How does this work?
You can set up any Cloudwatch alarm to be your trigger, this could be an application or infrastructure alarm e.g. CPU Utilization > 80% for over 5 minutes. 
Cloudwatch alarm is generated and notifies the SNS topic, this topic invokes a Lambda function that we call "MainFunction", extracts the alarm description that will be converted into speech by AWS Polly. The connect-1 is started by this Lambda function and based on the response the connect-2 is invoked. If team's first contact can resolve the issue connect-2 will not be invoked by the Lambda function. If the first person presses 2 (which means he cannot pick up the incident) the Lambda is invoked and a connect-2 will be started and second person will be called. The same is follwed for the third person.  

# How to setup the solution?
Step 1:
Create the Amazon Connect instance by following the aws provided doc: https://docs.aws.amazon.com/connect/latest/adminguide/gettingstarted.html
Note: As and when AWS will add support for Connect to Cloudfront, we will update our script and automate this step as well. 

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
[![Launch Stack](https://cdn.rawgit.com/buildkite/cloudformation-launch-stack-button-svg/master/launch-stack.svg)](https://console.aws.amazon.com/cloudformation/home#/stacks/new?stackName=connect&templateURL=https://s3.amazonaws.com/aws-connect-sf-poc/main.yaml)

Step 8:
Navigate to Cloudformation console and the depoyed stack's output section, copy the arn for second function and third function.

Step 9:
Navigate to https://NAME-YOU-PROVIDED.awsapps.com/connect/contact-flows select contact-1 in the GUI double click the invoke lambda function block and paste the arn of the second function. Press save and publish.

Step 10:
Navigate to https://NAME-YOU-PROVIDED.awsapps.com/connect/contact-flows select contact-2 in the GUI double click the invoke lambda function block and paste the arn of the third function. Press save and publish.

Step 11:
Create a cloudwatch alarm for the desired metric or any custom metric and put the informative alarm description. This description is spoken by the aws connect. Send the alarm notification to "connect" SNS topic. This is done during alarm creation step itself. 

###### Solution Architecture 
![Optional Text](https://github.com/sourcefuse/aws-connect/blob/master/connect-arch.png)

###### Connect Flow Diagram
![Optional Text](https://github.com/sourcefuse/aws-connect/blob/master/connect.png)


