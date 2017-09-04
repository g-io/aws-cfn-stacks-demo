# aws-cfn-stacks-demo
Demo of several ways to set up cloudformation stacks.
This sets up a minimal stack which is then later divided to show multiple ways of slicing and dicing stacks.
Remember that this will incur costs and also remember to tear down the resources later!

## Prerequisites
* python
* aws cli (pip install)
* sceptre cli (pip install)
* GNU make
* export AWS\_PROFILE=<profile\_with\_permissions\_to\_create\_resources> into your environment
* access to AWS web console to view all the different stacks and resources

## Basic docs
* http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/Welcome.html

* https://aws.amazon.com/blogs/devops/use-nested-stacks-to-create-reusable-templates-and-support-role-specialization/
* http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-stack.html

* https://github.com/cloudreach/sceptre
* https://sceptre.cloudreach.com/latest/docs/templates.html

## Play with...

### Single stack
This one sets up security group and instance in one simple template.

#### Notes:
* Change into dir
* Check and use the make targets

### Two independent stacks
Two independent stacks are created, with the one stack exporting a value that the other one imports to make use of it in a dynamic way

#### Notes:
* Change into dir
* Check and use the make targets

### Nested stacks
The two formerly independent stacks are now orchestrated by a master-stack and handeled as nested stacks

#### Notes:
* Change into dir
* Check and use the make targets
* S3-bucket is hardcoded, please change to your own needs if needed

### Sceptre with CloudFormation templates
Usage of sceptre to set up a dev environment of independent stacks. The dependencies are not managed by CloudFormation anymore, but by sceptre.

#### Notes:
Make sure you export your AWS\_DEFAULT\_REGION into the environment, because the config is set up to take it from there.
Example:
```
export AWS_DEFAULT_REGION=eu-west-1
```

Then launch and delete envs:

```
sceptre --var-file config/vars.yaml launch-env dev
sceptre --var-file config/vars.yaml delete-env dev
```
