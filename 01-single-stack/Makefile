STACK_NAME=dataprovisioning-test-dev

create:
	aws cloudformation create-stack \
            --stack-name $(STACK_NAME) \
            --template-body file://stack-test.yaml \
            --tags Key=team,Value=DataProvisioning Key=product,Value=test Key=environment,Value=dev
	aws cloudformation wait stack-create-complete \
            --stack-name $(STACK_NAME)

update:
	aws cloudformation update-stack \
            --stack-name $(STACK_NAME) \
            --template-body file://stack-test.yaml \
            --tags Key=team,Value=DataProvisioning,Key=product,Value=test,Key=environment,Value=dev
	aws cloudformation wait stack-update-complete \
            --stack-name $(STACK_NAME)

delete:
	aws cloudformation delete-stack \
            --stack-name $(STACK_NAME)
	aws cloudformation wait stack-delete-complete \
            --stack-name $(STACK_NAME)

describe:
	aws cloudformation describe-stacks \
           --query 'Stacks[?StackName==`$(STACK_NAME)`]'

recreate: delete create
