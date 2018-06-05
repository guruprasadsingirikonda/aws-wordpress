# AWS CloudFormation with EC2 RDS and Docker App
    
    
    
 # Setup AWSCLI console

 1. Login to AWS Management Console and Generate a new KeyPair. Save the downloaded key
 2. Configure AWS Command Line Interface (AWS CLI) with a new AWS Access Key and a secret generated on AWS  
 3. Update the stack.yml if you're using this template for your application
 4. Use AWS CLI to run create-stack command that'll create all the resources defined in the stack.yml
 5. Update the docker-compose app.yml if you're using this for your application
 6. Run docker-compose up -d in detach mode in Ec2 instance to run docker containers
 
 
 
 
# Commands

mkdir ~/aws-wordpress

git clone  git@github.com:guruprasadsingirikonda/aws-wordpress.git

cd aws-wordpress

#Create new KeyPair on AWS CLI and name it aws-key1 and

cd ~/Downloads/awsblog.pem 

#Change the permissions of download keypair  

chmod 400 awsblog.pem

#On AWS CLI, Create a new user with programatic access which will generate a new Access Key & Secret. With that

aws configure --profile demoapp
#Make sure to use the region name (us-west-2 or another) as the default for this profile 'demoapp'


aws cloudformation create-stack --profile demoapp --stack-name blog-stage --template-body file://$PWD/stack.yml

#After the stack creation is successful, Get the IP address or DNS of the AppNode EC2 instance

ssh -i aws-key1.pem ubuntu@<IP ADDRESS OR DNS OF THE EC2 INSTANCE>

#Point your local to EC2 instance

export DOCKER_HOST=tcp://<Ec2Ip>:2375
docker ps -a

docker-compose -f app.yml run --rm app rails db:migrate
docker-compose -f app.yml up -d
docker-compose -f app.yml ps
 
    
    
    
