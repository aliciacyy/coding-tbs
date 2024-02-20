---
label: Heroku
---

!!!
Information is accurate as of 20th Feb 2024
!!!

## Deploying Node.js application with Heroku

1. Create a new app
2. Follow instructions to deploy using Heroku Git

## Using your custom domain name from Route 53 with Heroku

### In Heroku
1. Go to Settings > Domains
2. Add your domain game (one with www and one without)
![](/static/heroku1.png)

### In AWS
1. Create a S3 bucket where the name is the same as your domain name without www
2. Go to Properties > Static website hosting
![](/static/heroku2.png)
3. Go to CloudFront and create distribution
   - For the "Origin Domain Name", select the S3 bucket you created. It should appear in the dropdown with the S3 website endpoint URL (not the bucket name).
   - Set "Viewer Protocol Policy" to "Redirect HTTP to HTTPS" to enforce SSL.
   - In "Alternate Domain Names (CNAMEs)", enter your root domain (e.g., `mydomain.com`).
   - Choose an SSL certificate that covers your root domain.
4. In Route 53: 
   - Add a CNAME record where the record name is with the www that points to the Heroku domain
   - Add an A record for root domain where the target is the Cloudfront distribution


## Reference
Reference of the ChatGPT response that helped me to solve the issue of not being able to use naked domain directly.

==- ChatGPT Response
```
Yes, you can use Amazon CloudFront and S3 to redirect your root domain (e.g., `https://mydomain.com`) to a `www` subdomain (e.g., `https://www.mydomain.com`). This is a common approach for handling domain redirections in AWS, leveraging S3's static website hosting feature for redirection and CloudFront for SSL/TLS support and global content delivery. Here's how to set it up:

### Step 1: Set Up an S3 Bucket for Redirection

1. **Create a new S3 bucket** with the exact name of your root domain (e.g., `mydomain.com`).

2. **Enable static website hosting** on the bucket:
   - Go to the bucket's Properties.
   - Find the "Static website hosting" section.
   - Select "Redirect requests".
   - In the "Target bucket or domain" field, enter your `www` subdomain (e.g., `www.mydomain.com`).
   - In the "Protocol" field, enter `https`.

3. **Bucket Policy**: Ensure the bucket's permissions allow public access (since it's serving a website). Update the bucket policy accordingly.

### Step 2: Create a CloudFront Distribution

1. **Create a new CloudFront distribution**:
   - For the "Origin Domain Name", select the S3 bucket you created. It should appear in the dropdown with the S3 website endpoint URL (not the bucket name).
   - Set "Viewer Protocol Policy" to "Redirect HTTP to HTTPS" to enforce SSL.
   - In "Alternate Domain Names (CNAMEs)", enter your root domain (e.g., `mydomain.com`).
   - Choose an SSL certificate that covers your root domain. You can use the AWS Certificate Manager (ACM) to create or import a certificate if you don't already have one.

2. **Finalize and create the distribution**. Note the CloudFront distribution's domain name (e.g., `d1234.cloudfront.net`) - you'll need it for the DNS configuration.

### Step 3: Configure Route 53

1. **Go to the Route 53 dashboard**, and select your hosted zone.

2. **Create or modify an A record for your root domain**:
   - Record name: `@` or leave blank for the root domain.
   - Type: `A – IPv4 address`.
   - Alias: Yes.
   - Alias Target: Select the CloudFront distribution you created.

3. **Ensure you have a CNAME record for your `www` subdomain** pointing to your Heroku app or wherever your primary content is hosted.

### Step 4: SSL/TLS and Testing

- Ensure that your SSL/TLS certificates are correctly set up in both Heroku and AWS Certificate Manager.
- After you've made these changes, it may take some time for DNS changes to propagate and for CloudFront to deploy.
- Once everything is propagated and deployed, accessing `https://mydomain.com` should redirect users to `https://www.mydomain.com` with the help of the S3 bucket redirection and CloudFront.

This setup leverages AWS services for a more integrated approach, especially useful if you're already using AWS for other aspects of your infrastructure.
```
