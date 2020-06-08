---
title: "CodeCommit"
weight: 23
pre: "<b>2-2. </b>"

---

### CodeCommit Setup and source code download

AWS CodeCommit is a fully managed source control service that hosts secure Git-based repositories. This service allows multiple teams to collaborate on code in a secure, highly scalable ecosystem. Since the actual work code is on Github, we will start moving this code to your CodeCommit Repository.

1.	let`s set up the code in Cloud9. Enter the following command in the terminal of Cloud9.

    ```bash
    git clone https://github.com/sykang169/ConcurrencySample.git
    ```

1. If the command is executed successfully, created a folder name concurrencysample in the file cloud9 file tree.
    ![CodeCommit01](/images/codecommit-master.png)

1. clone gets the master branch. If you look at the contents of the folder, there are no other files except the README.md file.
the real source code in develop, pull the develop branch. 

    ```bash
    cd ConcurrencySample
    git checkout origin/develop -b develop
    ```

1. You can see that a lot more files were created than the master. Now we will change the master and develop code to the codecommit's **concurrencysample** repository, which we created before in cloudformation stack.	
    ![CodeCommit02](/images/codecommit-develop.png)


1.	To check the output of CloudFormation, go to the CloudFormation console.

    go to the CloudFormation console : https://console.aws.amazon.com/CloudFormation

1.	Select **Stacks** from the left menu and select **CodeQuality-Workshop** you created. You can check the detailed information of the stack created here.
    ![CodeCommit02](/images/codecommit-cloudformation-select-stack.png)

1.	Select Outputs at the top of the stack details. There you **copy** the URL of CodeCommit that lab `a repository.
    ![CodeCommit02](/images/codecommit-cloudformation-stacks-output.png)

1. back to Cloud9. Check the url of the current origin in the previously created concurrencysample folder.
    ```bash
    git remote show origin
    ```
    Enter the command, you cant show the url of the currently set origin.
    ```bash
    remote origin
    Fetch URL: https://github.com/sykang169/ConcurrencySample.git
    Push  URL: https://github.com/sykang169/ConcurrencySample.git
    HEAD branch: master
    Remote branches:
        develop tracked
        master  tracked
    Local branches configured for 'git pull':
        develop merges with remote develop
        master  merges with remote master
    Local refs configured for 'git push':
        develop pushes to develop (up to date)
        master  pushes to master  (up to date)
    ```
    Change the url of origin to the address of the newly created codecommit at https://github.com/sykang169/ConcurrencySample.git.
  
    Entering the following in the terminal of Cloud9. **<YOUR_REPOSITORY-URL>** is the chagne CodeCommit copied from the Stack of CloudFormation.
    ```bash
    git remote set-url origin <YOUR-REPOSITORY-URL>
    ``` 
    After finished the command, check again with `git remote show origin`, and you can see that the URL of origin has been changed to your CodeCommit address.
    ```bash
    Fetch URL: <YOUR_REPOSITORY-URL>
    Push  URL: <YOUR_REPOSITORY-URL>
    HEAD branch: master
    Remote branches:
        develop tracked
        master  tracked
    Local branches configured for 'git pull':
        develop merges with remote develop
        master  merges with remote master
    Local refs configured for 'git push':
        develop pushes to develop (up to date)
        master  pushes to master  (up to date)
    ```

1. Now, we will push the code of Cloud9 to the changed CodeCommit Repository. First checkout to master and then push. CodeCommit's Repo doesn't have a any push yet, so the branch that was created first becomes the default branch. so you need to push master first.
    ```bash
    git checkout master
    git push
    ```
    Push develop in the same way.
    ```bash
    git checkout develop
    git push
    ```


-[Now let`s connect CodeGuru to CodeCommit.](/en/setup/codeguru-reviewer) 
