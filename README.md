# AWS Connect Solution For Alerts

# Need for this solution?
The purpose of this solution is to provide the way to get notified via automated calls on event of any failure. One may miss the text messages or slack messages during failure events. This solution calls the three provided contacts. For example on event of failure first person will be called, incase he cannot fix the issue or may be busy he can transfer the call to second person by choosing the suitable IVR options and so on. 

# How this works?
Cloudwatch alarm is generated and notifies to the sns topic, this topic invokes a lambda function we named as "MainFunction" extracts the alarm description as this text will be converted into speech by connect. The connect-1 is started by this lambda function and based on the response the connect-2 is invoked. If team's first contact can resolve the issue connect-2 will not be invoked by a lambda function. Else if the first person press 2 the lambda is invoked and a connect-2 will be started and second person will be called. The same is follwed for the third person.  

# How to setup the solution?
Step 1:
Create the amazon connect instance by following the aws provided doc: https://docs.aws.amazon.com/connect/latest/adminguide/gettingstarted.html

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
Navigate to cloudformation console and the depoyed stack's output section, copy the arn for second function and third function.

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


