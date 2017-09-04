STACK_NAME_SECGROUP=dataprovisioning-test-dev-security-group
STACK_NAME_INSTANCE=dataprovisioning-test-dev-instance

create-security-group:
	aws cloudformation create-stack \
            --stack-name $(STACK_NAME_SECGROUP) \
            --template-body file://stack-test-security-group.yaml \
            --tags Key=team,Value=DataProvisioning Key=product,Value=test Key=environment,Value=dev
	aws cloudformation wait stack-create-complete \
            --stack-name $(STACK_NAME_SECGROUP)

update-security-group:
	aws cloudformation update-stack \
            --stack-name $(STACK_NAME_SECGROUP) \
            --template-body file://stack-test-security-group.yaml \
            --tags Key=team,Value=DataProvisioning,Key=product,Value=test,Key=environment,Value=dev
	aws cloudformation wait stack-update-complete \
            --stack-name $(STACK_NAME_SECGROUP)

delete-security-group:
	aws cloudformation delete-stack \
            --stack-name $(STACK_NAME_SECGROUP)
	aws cloudformation wait stack-delete-complete \
            --stack-name $(STACK_NAME_SECGROUP)

describe-security-group:
	aws cloudformation describe-stacks \
           --query 'Stacks[?StackName==`$(STACK_NAME_SECGROUP)`]'

recreate-security-group: delete-security-group create-security-group

create-instance:
	aws cloudformation create-stack \
            --stack-name $(STACK_NAME_INSTANCE) \
            --template-body file://stack-test-instance.yaml \
            --tags Key=team,Value=DataProvisioning Key=product,Value=test Key=environment,Value=dev \
            --parameters ParameterKey=SecurityGroupName,ParameterValue=SecurityGroup-$(STACK_NAME_SECGROUP)
	aws cloudformation wait stack-create-complete \
            --stack-name $(STACK_NAME_INSTANCE)

update-instance:
	aws cloudformation update-stack \
            --stack-name $(STACK_NAME_INSTANCE) \
            --template-body file://stack-test-instance.yaml \
            --tags Key=team,Value=DataProvisioning,Key=product,Value=test,Key=environment,Value=dev \
            --parameters ParameterKey=SecurityGroupName,ParameterValue=SecurityGroup-$(STACK_NAME_SECGROUP)
	aws cloudformation wait stack-update-complete \
            --stack-name $(STACK_NAME_INSTANCE)

delete-instance:
	aws cloudformation delete-stack \
            --stack-name $(STACK_NAME_INSTANCE)
	aws cloudformation wait stack-delete-complete \
            --stack-name $(STACK_NAME_INSTANCE)

describe-instance:
	aws cloudformation describe-stacks \
           --query 'Stacks[?StackName==`$(STACK_NAME_INSTANCE)`]'

recreate-instance: delete-instance create-instance

create: create-security-group create-instance

update: update-security-group update-instance

delete: delete-instance delete-security-group

describe: describe-security-group describe-instance

recreate: delete create
