## Setup on EC2

VPC and subnet should be present. Tested on Ubuntu 14.04.

Add/ change below variables in ec2_create.yml

    keypair: KEY_PAIR
    instance_type: t2.micro
    security_group: NAME_OF_THE_GROUP_TO_BE_CREATED_OR_UPDATED
    image: ami-9abea4fb
    region: AWS_REGION
    vpc: VPC_ID
    subnet: SUBNET_ID

#### Create an instance

    ansible-playbook ec2_create.yml

#### Install nginx, mysql, jdk, tomcat and addressbook
    
    ansible-playbook -i hosts playbook.yml
    
Application can be accessed from IP or its public DNS.

#### Logstash setup
Use below pattern in tomcat/conf/server.xml valve settings and restart it.

    pattern="%h %l %u %t &quot;%r&quot; %s %b &quot;%{Referer}i&quot; &quot;%{User-Agent}i&quot; %A %p %D %S &quot;%{X-Forwarded-For}i&quot; &quot;%{SECURITY_LOGIN_NAME}s&quot;" />
    /opt/apache-tomcat-7.0.69/bin/shutdown.sh
    /opt/apache-tomcat-7.0.69/bin/startup.sh

Un-comment logstash role in playbook.yml and run

    ansible-playbook ec2_create.yml
    
    
