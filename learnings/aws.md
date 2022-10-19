---
label: AWS Services
---

!!!
Information is accurate as of 19th Oct 2022.
!!!

### Deploying Node.js application with AWS

1. Create an AWS Account
2. Go to Elastic Beanstalk and click "Create Environment"
3. Select "Web server environment"
![](/static/aws1.png)
4. Fill the following details: Application name, Environment Name, Domain (optional), Platform (see screenshot below) and click "Create enviornment"
![](/static/aws2.png)
5. Wait for environment to finish setting up, then you can access it from Environment.
6. To update and deploy the environment, use "Upload and deploy" button. (create a ZIP file of your source code)

### Buying a domain from AWS
1. Go to Route 53
2. Click on Domains > Register Domain
3. Choose your domain name and add to cart
4. Remember to verify your e-mail address after purchasing the domain
![](/static/aws3.png)
5. On clicking the link, you should see this:
![](/static/aws5.png)

### Add alias to the domain
1. Go to Route 53 > Hosted Zones > (your domain)
2. Click "Create Record"
3. Enabled the "Alias" switch
4. For "Route traffic to", select "Alias to Elastic Beanstalk environment", (your region) and the URL for the Elastic Beanstalk environment 
![](/static/aws4.png)

### Create SSL with Certificate Manager
1. Go to Certificate Manager
2. Click "Request" > Request a public certificate
3. Enter the domain name (not elastic beanstalk URL) and pick DNS validation and request.
4. (not sure if I did this) Go back to Route 53 > Hosted Zones > (your domain) and create a CNAME record, putting CNAME name as Record name and CNAME value as Value.

### Use SSL with Elastic Beanstalk
1. Go to Elastic Beanstalk > Configuration > Load balancer > Edit
2. In Listeners, click "Add listener" and fill the following:
![](/static/aws6.png)

Reference: https://medium.com/@jameshamann/configuring-your-elastic-beanstalk-app-for-ssl-9065ca091f49