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
