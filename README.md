# rundeck-aws-ssm-plugin
Rundeck Node Executor Plugin for AWS SSM.

This is a [Rundeck Plugin](https://docs.rundeck.com/docs/learning/tutorial/terminology.html#plugins) that allows you to execute commands on remote nodes via the AWS Systems Manager [SSM](https://docs.aws.amazon.com/systems-manager/latest/userguide/what-is-systems-manager.html) Run Command - specifically, the [RunShellScript](https://docs.aws.amazon.com/systems-manager/latest/userguide/walkthrough-cli.html#walkthrough-cli-example-1) command. This is particularly useful for teams already using SSM that do not want to use SSH within their environments.

#### 1. Rundeck server must have proper permissions to execute commands through SSM. 
You can do this by adding the **AmazonSSMAutomationRole** IAM Policy to the role associated with your Rundeck instance (either your API creds or IAM Role assigned to your Rundeck instance - if Rundeck is installed on an EC2). 

#### 2. Download this repo and create a zip file of the whole directory.
    zip -r rundeck-aws-ssm-plugin.zip rundeck-aws-ssm-plugin

#### 3. Place the zip file into the `libext` directory on your Rundeck server.
   More details can be found in Rundeck's documentation on [installing plugins](https://docs.rundeck.com/docs/administration/configuration/plugins/installing.html#installation). 
    
    
#### 4a. To set this as the Node Executor for individual nodes, add the following to the custom attributes of your node(s) definition:
    node-executor: ssm-executor
    
#### 4b. Optionally set this to be the default method of Node Execution at the Project level:
  Set the [Default Node Executor](https://docs.rundeck.com/docs/manual/project-settings.html#edit-configuration) in the GUI to **AWS SSM / Node Executor**, or manually add `service.NodeExecutor.default.provider=ssm-executor` to the project config file.

#### 4c. Optionally set this to be the default method of Node Execution at the Framework level (system wide): 
  Set `service.NodeExecutor.default.provider=ssm-executor` in `framework.properties`
