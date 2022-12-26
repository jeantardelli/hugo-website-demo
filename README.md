[![AWS CodeBuild Deploy](https://codebuild.us-east-1.amazonaws.com/badges?uuid=eyJlbmNyeXB0ZWREYXRhIjoidGtwTzZSYXRtU3lFMTZPUkJySk00MVVGY2JHOExROXgzTFRPdC83QzBGVzVSTmJaenRsTEc2VXlRY0lBejYxWU9VNFg0NWZQR3FQbjIrVFVxSUdCb2NNPSIsIml2UGFyYW1ldGVyU3BlYyI6InA3WGFuUUpuQXpSN3ZHRmgiLCJtYXRlcmlhbFNldFNlcmlhbCI6MX0%3D&branch=main)

# hugo-website-demo
This is a demo hugo CD project.

You can see this running on [cuestamucho.link](http://cuestamucho.link)
Complete tutoria here: https://www.youtube.com/watch?v=xiodvLdPnvI

1. Download wget https://github.com/gohugoio/hugo/releases/download/v0.109.0/hugo_0.109.0_Linux-64bit.tar.gz

2. Create a bin directory on AWS Cloud9
```
mkdir -p ~/bin
```

3. Check hugo is installed:
```
hugo version
```

4. Create a quickstart site:
```
hugo new site quickstart
```

5. Go to /quickstart and add theme submodule:
```
git submodule add https://github.com/budparr/gohugo-theme-ananke.git themes/ananke
```

6. Echo out the config file:
```
echo 'theme = "ananke"' >> config.toml
```

7. Create a new post:
```
hugo new posts/my-first-post.md
```

8. Run Hugo locally in Cloud9

We have to to run hugo as a development server. This step will require us to open up a port on EC2 security groups.

A. Open a new tab on the AWS Console and type in EC2 and scroll down to security groups and look
for the security group with the same name as your AWS Cloud9

B. Open up via new TCP rule port 8080 and the edit button. This step will allow us to browse to
port 8080 to preview our website as we develop it locally on AWS Cloud9.

C. Navigate back to AWS Cloud9 and run the following command to find out the IP Address (we
will use this IP Address when we run hugo ). Note you can also find your IP Address from the AWS
Console for EC2)

```
curl ipinfo.io
```

D. Run `hugo` with the following options; you will need to swap this IP Address out 
with the one you generated earlier. Notice that the `baseURL` is essential so you 
can test navigation.

```
hugo serve --bind=0.0.0.0 --port=8080 --baseURL=http://{your_ip}/
```

E. Open a new tab in your browser and type paste in the URL in the output.

**Step6: Create Static Hosted Amazon S3 website and deploy to the bucket.**

The next thing to do is to deploy this website directory to an AWS S3 bucket. You can follow the
instructions here on creating an s3 bucket and set [it up for hosting](https://docs.aws.amazon.com/AmazonS3/latest/user-guide/static-website-hosting.html).

You have to buy a domain for that :) 

**Step7: Deploy the website manually before it becomes fully automated**

With automation, it is essential to manually write down the steps for a workflow before fully
automating it. The following items will need confirmation:

A. The config.toml will need to be edited. Note that your s3 bucket URL will be different.

B. Now, you can deploy by using the built-in hugo deploy command. The deployment command
output should look like this after you run hugo deploy.

The contents of the AWS S3 bucket should contains now all the files.

**Step8: Check into Github**

Log in into Github and create a new repo (and add .gitignore)

A. In AWS Cloud9, in the quickstart directory, create a Makefile with a clean command. This will rm
-rf the public HTML directory that hugo creates. You don’t want to check this into source control.

```
clean:
    echo "deleting generated HTML"
    rm -rf public
```

B. Now run make clean to delete the public directory and all of the source code hugo generated
(don’t worry, it regenerates HTML anytime you run hugo)

Add the source code and push to Github

**Step9: Continuous Delivery with AWS CodeBuild**

Now it is time for the final part. Let’s continuously setup delivery using AWS CodeBuild. This
step will allow changes that get pushed to Github to deploy automatically.

A. Go to AWS CodeBuild and create a new project. Note create a build in the same region you made your
   bucket: i.e., N. Virginia!
   
B. The source code section should look similar to this screenshot. Note the webhook. This step will do
   continuous delivery on changes
   
C. After you create the build navigate to the “Build details” section and select the service role. This
where the privileges to deploy to S3 will be setup. Attache the S3 Full Access privileges.

D. Create a 'buildspec.yaml' file. 

Now every time you make changes to the content directory, it will “auto-deploy” as shown.
  
