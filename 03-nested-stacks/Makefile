STACK_NAME_MASTER=dataprovisioning-test-dev

create:
	aws s3 cp stack-test-instance.yaml s3://fcst-nwp.ukmo.ukv.dv.s3.mg/sandbox/stack-templates/
	aws s3 cp stack-test-security-group.yaml s3://fcst-nwp.ukmo.ukv.dv.s3.mg/sandbox/stack-templates/
	aws cloudformation create-stack \
            --stack-name $(STACK_NAME_MASTER) \
            --template-body file://stack-test-master.yaml \
            --tags Key=team,Value=DataProvisioning Key=product,Value=test Key=environment,Value=dev
	aws cloudformation wait stack-create-complete \
            --stack-name $(STACK_NAME_MASTER)

update:
	aws s3 cp stack-test-instance.yaml s3://fcst-nwp.ukmo.ukv.dv.s3.mg/sandbox/stack-templates/
	aws s3 cp stack-test-security-group.yaml s3://fcst-nwp.ukmo.ukv.dv.s3.mg/sandbox/stack-templates/
	aws cloudformation update-stack \
            --stack-name $(STACK_NAME_MASTER) \
            --template-body file://stack-test-master.yaml \
            --tags Key=team,Value=DataProvisioning,Key=product,Value=test,Key=environment,Value=dev
	aws cloudformation wait stack-update-complete \
            --stack-name $(STACK_NAME_MASTER)

describe:
	aws cloudformation describe-stacks \
           --query 'Stacks[?StackName==`$(STACK_NAME_MASTER)`]'

delete:
	aws cloudformation delete-stack \
            --stack-name $(STACK_NAME_MASTER)
	aws cloudformation wait stack-delete-complete \
            --stack-name $(STACK_NAME_MASTER)

recreate: delete create
