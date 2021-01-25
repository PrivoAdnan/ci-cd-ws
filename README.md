Client has 1 app:

    One standard web server that will be stood up in an Autoscaling group behind and an ALB and WAF.  
  
    They want a CI/CD pipeline for updates.  All infrastructure will be maintained in Cloudformation.
    Openvpn Host, Bastion Host, App Staging Instance, ALB, Production Web Server Autoscaling Group, and Codedeploy must be configured.

Task 1 -- Git intro

    Run through a few of the levels here:  https://learngitbranching.js.org/

    You'll need to know how to clone a repo, create a new branch, commit, push, merge, and rebase.

Task 2 -- Clone this repo and setup your branches

    Clone this repo and Create 2 branches:  username-master and username-wip
    You'll make your changes and test them from the username-wip branch and merge them into the username-master branch for practice.  The original master branch will stay untouched. 

    Submitting pull requests with corrections and suggestions for future training are welcome and expected!   Please go nuts in your copy of the readme.  Document every question you had to ask, where knowledge gaps were or documentation was lacking, add links to glue articles or aws articles that you found helpful.  
    Do a git push for each branch so they'll exist in the remote repository.

Task 3 -- Cloudformation VPC

    Privo standard VPC Review
    Deploy the vpc template.

Task 4 -- EC2 instances

    Using the generic ec2 stack that exists, make a template for a bastion host and a app host.

    Create a bastion host in the default VPC in dev.
    Name host appropriately (username-bastion)
    Set ingress/SG appropriately
    
    Create another instance with private-only IP in appropriate subnet
    Name, etc...correctly (username-app)
    
    Verify connectivity between bastion and private instance
       - make security group corrections in the templates as necessary, commit changes
    
    In the templates, Resize disk on private only instance and extend volume, commit changes
    
    See what else you can do.  
    
    Deploy the amazon-linux-openvpn template
    
    Commit your changes and push your username-wip branch.
    Make a pull request to merge username-wip with username-master
    
    Stop your app instance and create an encrypted ami from it and copy to multiple regions (name it username-ami)

Task 5 -- ALB

    Launch ALB/WAF Template

Task 6 -- Add hosts to new VPC

    Config userdata in launch config to install needed services for basic website on hosts
    Ensure an index.html is in /var/www/html/
    Verify basic website is available at address of ALB
    Push code to same github repo

Task 7 -- Add database tier

    Launch RDS in private data subnet
    Verify connectivity over openvpn with docker container

Task 8 -- Codedeploy

    Either do the CD or create new launch config that installs wordpress
    Connect wordpress to RDS instance
    Verify dummy wordpress site works
    Push code to same github repo

Task 9 -- route53

    Create CNAME for ALB to a real domain name.  Fire a flare here.
        
EXTRA TASKS/WIP

Task 10 -- Codedeploy with Codepipeline
    
    Create a pipeline in CodePipline with a hook to Github that pushes commited changes in the repo to CodeDeploy

Task 11 -- Create 2nd VPC and setup VPC Peering

    Use previous code to launch VPC with 10.200.x.x/16
    Create bastion host
    Peer this VPC to the 1st VPC you created
    Modify SG and NACL as necessary
    Ping between bastion hosts to verify traffic
    Document all of this stuff in the same glue onboarding organization
    Commit your changes to the repo

Task 12 -- ECS Cluster

Task 13 -- ECS Cluster codepipeline

Task N+1 -- Delete all the things.
