# SETUP git Deployment on push

## REQUIREMENTS
* git must be installed on both machines



### TODO 
1) Setup ssh to server 
2) Reconnect to server through ssh
   1) create a ssh key
   2) copy key to server
   3) ssh-copy-id username@website.com
   4) login ssh username@website.com


   5) copy files to remote 
      1) scp text.html user@server.com:/var/www


   6) copy folders to remote 


3) setup git deployment via ssh
   1) ssh to server
   2) initialize a bare git 
        git init --bare projectName.git

   3) create post-receive in /git/hooks
        cd projectName.git/hooks
        nano post-receive
   4) create post-receive in /git/hooks
      1) CREATE AND SAVE POST-RECEIVE

        #!/bin/sh

        # --work-tree=/path/to/project/location ==== CHECKOUT FILES TO THIS location
        # --git-dir=/path/to/git/dir
        
        #CHECKOUT
        git --work-tree=/path/to/project/location --git-dir=/path/to/git/dir checkout -f

        # INSTALL dependencies
        cd /project/folder
        npm install

        console.log("
            ####################################
            ##  PROJECT UPLOADED & DEPLOYED   ##
            ####################################
        ")

        #Restart app
        pm2 reload project/dir


        # CTRL+O saves the file
        # CTRL+X to exit

   5) Activate post-receive
        chmod +X post-receive 
   6) ADD remote repo to local repo
        git remote add prod user@server.com:/path/to/git/location
   7) 