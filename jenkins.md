## Continuous Integration/Continuous Deployment 

![alt text](cicd.png)

The diagram above displays the CI/CD Pipeline. 
- CI refers to **automating the integration of code changes**. For example, if a group of developers are making changes to a code, CI automatically tests these codes to make sure it doesn't break anything. This helps catch bugs and issues early, leading to more stable and reliable software.
- CD refers to **automating these tested and approved changes to the live environment**. 
- Together CI/CD creates a pipeline that takes code from the developers machines to the live environment with **minimal manual intervention.** 

## Navigating Jenkins

### Creating a job in Jenkins

**Step 1.** Log In to Jenkins <br>
**Step 2.** Log in using your credentials. <br>
**Step 3.** Create a New Job: From the Jenkins dashboard, click on "New Item" or "Create New Job" on the left-hand side. <br>

![alt text](new.png)

**Step 4.** Enter a name for your job and select the type of job you want to create. <br>
**Step 5.** Select Freestyle project <br>

![alt text](name.png)

**Step 6.** Check `Discard old builds` <br>
**Step 7.** `Max # of builds to keep: 3` <br>

![alt text](old.png)

**Step 8.** Press ok <br>

### Testing Jenkins - does Jenkins have the env required for our deployment?

Step 1. Follow the above steps <br>
Step 2. Navigate to `Build` <br>
Step 3. Select `Execute Shell` <br>
Step 4. Enter the commands ` whoami uname -a` <br>
Step 5. Enter `Save` <br>

### Triggering the job manually

**Step 1.** Locate the job by using the dropdown and select `Build now` <br>

![alt text](buildnow.png)

![alt text](build.png)

**Step 2**. Navigate to the # use the drop down and select `console output` <br>
**Step 3.** You will now be able to see the env required for deployment 

### Configuring Job already made

**Step 1:** Select your job <br>
**Step 2:** Select `configure`