## Webhooks, Jenkins & CI/CD

![alt text](Images/diagram.png)

### What are Webhooks?

webhooks are a mechanism for one system to notify another system about events or updates in real-time. 

Webhooks allow different tools and services to communicate and automate processes seamlessly.

### Creating a Webhook

**Step 1:** Navigate to your repository containing the app
- Select `Settings`

![alt text](Images/settings.png)

**Step 2:** Navigate to Webhooks and Click `Webhooks`
- Then select `Add webhook`

![alt text](Images/webhook1.png)

**Step 3:** Set up configurations 

- Payload URL: Enter Jenkins URL followed by `github-webhook/`
- Content type: application json

![alt text](Images/pay.png)

**Step 4:** Which events would you like to trigger this webhook?
- Check `let me select individual events`
- Scroll to the bottom and check `Pull requests`

**Step 5:** press `Save`

Your webhook is now setup, and will be triggered when a change is made locally. 

### Creating a Job for Continuous Integration (CI)

**Step 1:** log into Jenkins and click 'New Item'
- Enter a name 
- click 'Freestyle project', then okay 

**Step 2:** General 
- Enter a description
- `Discard old builds: 3`

![alt text](Images/s3.png)

**Step 3:** Check `GitHub project`
- Enter your repo HTTPS URL

![alt text](Images/s4.png)

**Step 4:** Office 365 Connector 

- Check `Restrict where this project can be run`
- Label Expression: `sparta-ubuntu-node`

![alt text](Images/s5.png)

**Step 5:** Source Code Management
- Check `Git`
- Enter your SSH URL for your repository
- Credentials: select your private key 

**Step 6:** Source Code Management
- Branch Specifier: `*/dev`

![alt text](Images/s6.png)

**Step 7:** Build Triggers
- Check: `GitHub hook trigger for GITScm polling`

![alt text](Images/s7.png)

**Step 8:** Build Environment 
- Check `Provide Node & npm bin/folder to PATH`

![alt text](Images/s8.png)

**Step 9:** Build
- Enter the following commands 

```
cd app
npm install
npm test
```

![alt text](Images/commands.png)

**Step 10:** Post-build Actions

![alt text](Images/pba1.png)

### Creating a job for a dev to main merge 

**Step 1:** Create a new job `New Item`
- Add `Description`
- `Check Discard old buils: 3`
- Check `GitHub project`
- Enter your repo HTTPS URL
- Check `Restrict where this project can be run`
- Enter: `sparta-ubuntu-node`
- Check `Git`
- Add your repo SSH URL, select your private key
- Branches to build `*/dev`

**Step 2:** Select `Add Additional Behaviours`
- Then select: `Merge before build`
- Enter Name of repository: `origin`
- Branch to merge to `main`

![alt text](Images/merge.png)

**Step 3:** Build Triggers
- Leave all unchecked

**Step 4:** Build Environment
- Check `SSH Agent`

![alt text](Images/ssh.png)

**Step 5:** Post-build Actions
- Select `Git Publisher`
- Check `Merge Results`
- Then press Save

![alt text](Images/save.png)

**Step 6:** Navigate to GitBash terminal 
- Change main to Dev

```
git branch dev
```

**Step 7:** Make a change in your local repository
- Commit changes
- Push to GitHub
- Whilst pushing Jenkins will be triggered and allow dev to merge to main

### Creating Jenkins Continuous Deployment pipeline

**Step 1:** Creating a new job `New Item`
- Log into Jenkins 
- Select `New Item`
- Create a name `Samiha-cd`
- Configure Office 365 Connector, Source Code Management, Build Triggers, Build Environment

**Step 2:** Triggering the New Job from Your Merge Job
- Navigate to the your 2nd job created
- Select a `post-build action`
- Select: `Build other projects`
- Projects to build: `Samiha-cd`

**Step 3:** Allowing Jenkins to SSH into EC2 Instance

- Set up SSH access for Jenkins to your EC2 instance.

- Add the -y commands so you don’t need to manually allow the SSH into your instance.

**Step 4:** Copying the App Code

**Step 5:** cd into the app folder

**Step 6:** Run npm install

**Step 7:** Install Node.js

**Step 8:** Verify the Code via SSH

**Step 9:** Modify the Application Name - Altering the name of `Sparta` to Samiha


