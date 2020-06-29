# Deploying Your First NodeJS Web App Part 1: Setting up DigitalOcean
Congratulations, you’ve finished developing your first NodeJS web app and now you want to publish it on the web. If you’re still in the development process however, then you may find my *XYZ NodeJS web app* guide helpful. 

There are many hosting platforms you can use to deploy your NodeJS web app such as Heroku, Vultr, Linode, Google Cloud Platform and Amazon Web Services.*Link to the platforms* We will be using DigitalOcean because it’s very popular, simple to use and good value.

## Setting up DigitalOcean

First, create an account on the DigitalOcean platform. There are discount codes available to add free credit to your account such as the code available in the Github Student Developer Pack. Be aware that you can only redeem one code per account.

Second, you need to create a droplet. A droplet is a VPS (Virtual Private Server.) It’s similar to a Linux VM which is hosted on a server farm somewhere. Once you’ve logged into your account, go to Droplets under the Manage heading and click Create and Droplets. 

You can leave most of the settings as the default but change the plan to the basic $5 a month which contains enough resources for your app. You can scale this up later if needed. 

Also, choose the datacenter closest to the target audience of your app and change the authentication to password. While password authentication is less secure (SSH Keys is recommended), it’s much easier to setup so for your first drop we’ll use that. 

All that’s left now is to pick a name (hostname) and click Create Droplet.

## Connecting to your Droplet
Shortly afterwards, you’ll receive an email containing the username and password of your droplet which you’ll use to login. 

Back on the DigitalOcean website, under Droplets, click the name of your newly created droplet and then on Console. This will open a new tab that will let you control your droplet. Alternatively, you can use any SSH client with the IP address and user credentials contained in the email. *Link to an article on SSH (see if Section has any already)*

On your first login, since you used password authentication, it will prompt you to set a new password. A great way to generate secure passwords and store them is a password manager like LastPass. *Link here*  

## Deploying Your NodeJS Web App
First, you’ll need to copy the code for your web app to your Droplet. If you’re using source control such as Git *Link to Section article on Git* then it’s a simple as installing git using `apt-get install git -y`  and then using the git clone command  `git clone (link to your repository)` and then add the link to your repository at the end.

Second, you’ll need to install Node. Type:

```bash
curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash -
sudo apt-get install -y nodejs
```

Third, you’ll need to install the node modules (dependencies) for your web app. If you installed all your modules with `-save` at the end which saves them to the package.json file then just type `npm install` and press enter. 

If not, when you run `npm start`  an error will appear with module not found. Type `npm install (module name)`  and press enter and then try running `npm start`  again. Repeat the process until the error disappears. 

If you need to install MongoDB (if you’ve created a MongoDB database), then follow these [instructions](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/#install-mongodb-community-edition).

Finally, type `npm start`  to start your web app. Now that your web app is running, in a new browser tab, type the IP Address of your droplet (found in the email that DigitalOcean sent when you created the droplet) followed by a colon and the port your app runs on. For example, `167.172.54.51:8080`.

If you’re using an Express web server (which if you followed my *Node JS Web App Guide*) you did, you’ll find the port number located in the  `app.listen()`  line inside the server.js file. For example,  `app.listen(8080)`  which is a common port used. 

Congratulations, your first NodeJS web app should be displayed in your web browser which is running on your DigitalOcean droplet.

Continue on to Part 2 to discover how to connect a domain name to the droplet (and thus web app) and how to keep the web app running using a process manager.