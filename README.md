# Cloud Computing & DevOps – Task 1
## Static Portfolio on Amazon S3 + CloudFront (HTTPS)

This project is a responsive, single-page portfolio built with HTML and CSS. It includes a hero section with a call-to-action, About section, three project cards, contact links and a footer. It uses Google Fonts and Font Awesome.

## 1. Files
- `index.html` – page content and layout
- `styles.css` – responsive styling
- `assets/` – place any additional images or assets here
- `bucket-policy.json` – example public-read policy for the S3 website-endpoint approach

## 2. Personalize before publishing
Search the files and replace:
- `Your Name` / `YN` with your preferred name or initials
- `your.email@example.com` with your email address
- `yourusername` with your GitHub and LinkedIn usernames
- Project descriptions and skills with accurate details about your own work

The three project cards are starter examples. Edit them so they accurately represent projects you have completed.

## 3. Preview locally
Open `index.html` in a browser. For a local development server, run:
```bash
python -m http.server 8000
```
Then visit `http://localhost:8000`.

## 4. Push to GitHub
Create a new GitHub repository, then run these commands from this project folder:
```bash
git init
git add .
git commit -m "Create portfolio website"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPOSITORY.git
git push -u origin main
```
Replace the remote URL with your repository URL.

## 5. Host on Amazon S3 (website endpoint method in the assignment)
1. Sign in to the AWS Management Console and open **Amazon S3**.
2. Create a globally unique bucket name, for example `yourname-portfolio-2026`.
3. Open **Properties → Static website hosting → Edit**. Enable hosting, choose **Host a static website**, set the index document to `index.html`, and save.
4. Open **Permissions → Block public access**. For this public website-endpoint method, turn off the bucket-level Block Public Access settings. Confirm the warning only after understanding that objects will be publicly readable.
5. Open **Permissions → Bucket policy**. Replace `YOUR_BUCKET_NAME` in `bucket-policy.json` with your bucket name and paste the policy.
6. Upload `index.html`, `styles.css`, and the `assets/` contents to the bucket root.
7. Open the **Bucket website endpoint** shown under Properties and test the site.

### Example bucket policy
The included `bucket-policy.json` grants public `s3:GetObject` access to objects in this bucket. Use it only for the public S3 website-endpoint approach described above. Do not use this policy for a private bucket.

## 6. Configure CloudFront with HTTPS
1. Open **CloudFront → Create distribution**.
2. For the origin, use the S3 **website endpoint** shown in the S3 bucket's Static website hosting properties. Select it as a custom origin (not the S3 REST origin).
3. Set the viewer protocol policy to **Redirect HTTP to HTTPS**.
4. Allow `GET` and `HEAD` methods. Keep caching enabled.
5. Set the default root object to `index.html`.
6. Create the distribution and wait until its status is **Deployed**.
7. Open the CloudFront distribution domain name (`https://...cloudfront.net`) and verify the site loads over HTTPS.

Note: With an S3 website endpoint as a CloudFront custom origin, the S3 website endpoint itself uses HTTP and the bucket content is public. CloudFront provides HTTPS to visitors. For a stronger production design, use a private S3 bucket with CloudFront Origin Access Control (OAC) and an S3 REST origin; this is a different setup and does not use the S3 website endpoint as the origin.

## 7. Update the website after edits
After uploading changed files to S3, create a CloudFront invalidation for:
```text
/*
```
This asks CloudFront to fetch the updated files instead of serving cached copies.

## 8. Evidence to capture for submission
Take genuine screenshots from your own AWS account:
- S3 bucket showing the uploaded website files
- S3 Static website hosting properties and website endpoint
- S3 bucket policy page
- CloudFront distribution showing **Deployed**, its distribution domain name and HTTPS configuration
- The live website opened using the CloudFront `https://` URL
- GitHub repository containing the source files

Do not use sample or fabricated screenshots. Add the screenshots to your submission PDF or ZIP.

## 9. Final submission checklist
- [ ] Personalized `index.html` and `styles.css`
- [ ] Assets uploaded to GitHub
- [ ] GitHub repository URL included in the submission
- [ ] S3 bucket created and website tested
- [ ] Bucket policy configured
- [ ] CloudFront distribution deployed
- [ ] HTTPS CloudFront URL tested
- [ ] Screenshots captured from the actual AWS account
- [ ] This README updated with your actual bucket, GitHub and hosted URLs
