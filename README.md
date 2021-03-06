# Azure Active Directory OIDC Web Sample

This Node.js app will give you with a quick and easy way to set up a Web application in node.js with Express using OpenID Connect. The sample server included in the download are designed to run on any platform.

We've released all of the source code for this example in GitHub under an MIT license, so feel free to clone (or even better, fork!) and provide feedback on the forums.

## Forked Version Notes

The changes are mainly cosmetic, using Bootstrap and Fontawesome to make the app look more presentable.
The default `config.js` file has been renamed `config.js.sample` preventing accidental checkin of secrets into Git. Before starting copy and rename the .sample file back to `config.js` and edit with your configuration as described in step 4.

## Quick Start

Getting started with the sample is easy. It is configured to run out of the box with minimal setup.

### Step 1: Register an web application in B2C Azure AD Tenant

If you don't have an Azure AD B2C Tenant yet, please [create one](https://azure.microsoft.com/en-us/documentation/articles/active-directory-b2c-get-started/).

Next let's register an web application in your tenant.

* In Azure port of your B2C tenant, use the search bar & search for 'Azure AD B2C', click on it, and you will be redirected to the B2C settings blade. Pin it to your dash you will be using it a lot.

* Click **Applications**, then click **Add**. Enter a name like 'my_b2c_app', and switch the **Web App / Web API** option to *yes*. After that, enter `http://localhost:3000/auth/openid/return` into the 'Reply URL' field, click **Create**. 
* Then go into your new app, and into the **Keys** blade and click **Generate key** to generate a app key, and save it somewhere. This app key is the *clientSecret* of your application.

* Click **Properties**, copy the **Application ID** field and save it somewhere. This value is the *clientID* of your application. Come out of the app and return to the main B2C blade 

* Now let's add some policies we will use for this sample. In the B2C blade, add four policies; sign-in policy, a sign-up policy, a profile-editing policy and a password-reset policy. When you add the policies, you must use the names as follows:
  - `signin` - Sign-in policy
  - `signup` - Sign-up policy
  - `updateprofile` - Profile editing policy
  - `resetpassword` - Password reset policy 
 
For **Identity providers**, choose `Email signup` on the sign-up policy, for the other three choose `Local Account SignIn`  
For **Application claims** on all four policies, choose `Email Address`, `User's Object ID` & `Display Name`. 
For **Sign-up attributes** (signup policy) choose `Email Address`  
For **Profile attributes** (updateprofile policy) choose `Display Name` and any other fields you wish the user to be able to set.

* Now we have a B2C web application and policies registered. Note that Azure AD adds a `B2C_1_` prefix automatically to all policy names, so the policy names we will use are actually `B2C_1_signin`, `B2C_1_signup`, `B2C_1_updateprofile` and `B2C_1_resetpassword`. 

### Step 2: Download node.js for your platform
To successfully use this sample, you need a working installation of Node.js.

### Step 3: Download the Sample application and modules

Next, clone the sample repo and install the NPM.

From your shell or command line:

* `$ git clone git@github.com:AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS.git`
* `$ npm install`

### Step 4: Configure your server

* Provide the parameters in `exports.creds` in config.js as instructed.

* Update `exports.destroySessionUrl` in config.js, using your tenant name and signin policy name. If you want to redirect the users to a different url after they log out, update the  `post_logout_redirect_uri` part as well.

* Set `exports.useMongoDBSessionStore` in config.js to false, if you want to use the
default session store for `express-session`. Note that the default session store is
not suitable for production, you must use mongoDB or other [compatible session stores](https://github.com/expressjs/session#compatible-session-stores).

* Update `exports.databaseUri`, if you want to use mongoDB session store and a different database uri.

* Update `exports.mongoDBSessionMaxAge`. Here you can specify how long you want
to keep a session in mongoDB. The unit is second(s).

### Step 5: Run the application

* Start mongoDB service.

If you are using mongoDB session store in this app, you have to install mongoDB and start the service first. If you are using the default session store, you can skip this step.

* Run the app.

Use the following command in terminal.

* `$ node app.js`

**Is the server output hard to understand?:** We use `bunyan` for logging in this sample. The console won't make much sense to you unless you also install bunyan and run the server like above but pipe it through the bunyan binary:

* `$ npm install -g bunyan`
* `$ node app.js | bunyan`

### You're done!

You will have a server successfully running on `http://localhost:3000`.

### Acknowledgements

We would like to acknowledge the folks who own/contribute to the following projects for their support of Azure Active Directory and their libraries that were used to build this sample. In places where we forked these libraries to add additional functionality, we ensured that the chain of forking remains intact so you can navigate back to the original package. Working with such great partners in the open source community clearly illustrates what open collaboration can accomplish. Thank you!


## About The Code

Code hosted on GitHub under MIT license
