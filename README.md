# docker-demo
its a docker demo code

Steps and code flow.
1.  Make a bridge connection or take clone a project from github
2.  Then I use AWS EC2 service for the hosting in CI/CD.
3.  So we will create a EC2 instance in AWS accout with
    in OS ubuntu
   key access as SSH key created and downloaded to access EC2 server
   verify the inbound port 22 as associate to SSH
    can add additional ports as per the requirenment in security group inbound
   then Launch instance

4.  change the protection for SSH key which we have downloaded with `"chmod 400 /home/ubuntu/Downloads/key_user.pem"`
5.  Connect to the EC2 server with this command `"ssh -i /path/to/your/key.pem ubuntu@<EC2_PUBLIC_IP>"`
6.  Download all the docker dependencies in EC2 server and can clone of that git projects.
7.  Create the `SSH key` for connecting EC2 to github `"ssh-keygen -t rsa -b 4096 -C "your_email@example.com" -f ~/.ssh/ci-ec2-key -N """`  with perhapse disable use for CI/CD automation.
8.   #### Add the public key (ci-ec2-key.pub) to your EC2's ~/.ssh/authorized_keys.
9. 
    #### Add the private key (ci-ec2-key) to your GitHub Secrets as EC2_SSH_KEY
   
    ### OR
    Go to your GitHub repo.
    #### Navigate to Settings → Secrets and Variables → Actions.
    Add these secrets:
    `AWS_HOST` → Your EC2 instance public IP.   
    `AWS_SSH_KEY` → Paste your private SSH key (~/.ssh/id_rsa).

10.  copy public key to SSH for git push
    cat ~/.ssh/id_rsa.pub
    #### Go to: GitHub → Settings → SSH and GPG Keys → New SSH Key → Paste the key → Save
11. Test SSH Connection

    `ssh -T git@github.com`
    If successful, you will get:
    
    Hi ankitkalyaa! You've successfully authenticated, but GitHub does not provide shell access.
    ### Change Remote URL
    Switch your remote from HTTPS to SSH:

    `git remote set-url origin git@github.com:ankitkalyaa/docker-demo.git`

12.  Add the CI/CD deploy.yml file in the .github/workflow/deploy.yml path and push the code to github.
13.  # sucessfuly deploye CI/CD automation 
