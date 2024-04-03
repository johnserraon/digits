![](https://raw.githubusercontent.com/johnserraon/digits/cleanup/doc/digits-landing-page.png?token=GHSAT0AAAAAACNAL4U5WM6L3GOHWUGO3THKZQM6GXQ)

digits is a Meteor application that allows registered users to create their own address book of business contacts.


## Installation

First, [install Meteor](https://www.meteor.com/install).

Second, go to [https://github.com/ics-software-engineering/meteor-application-template-react](https://github.com/ics-software-engineering/meteor-application-template-react), and click the "Use this template" button. Complete the dialog box to create a new repository that you own that is initialized with this template's files.

Third, go to your newly created repository, and click the "Clone or download" button to download your new GitHub repo to your local file system.  Using [GitHub Desktop](https://desktop.github.com/) is a great choice if you use MacOS or Windows.

Fourth, cd into the app/ directory of your local copy of the repo, and install third party libraries with:

```
$ meteor npm install
```

## Running the system

Once the libraries are installed, you can run the application by invoking the "start" script in the [package.json file](https://github.com/ics-software-engineering/meteor-application-template-react/blob/master/app/package.json):

```
$ meteor npm run start
```

The first time you run the app, it will create some default users and data. Here is the output:

```
 meteor npm run start 

> meteor-application-template-react@ start /Users/carletonmoore/GitHub/ICS314/meteor-application-template-react/app
> meteor --no-release-check --exclude-archs web.browser.legacy,web.cordova --settings ../config/settings.development.json

[[[[[ ~/GitHub/ICS314/meteor-application-template-react/app ]]]]]

=> Started proxy.                             
=> Started HMR server.                        
=> Started MongoDB.                           
I20220529-12:09:18.384(-10)? Creating the default user(s)
I20220529-12:09:18.389(-10)?   Creating user admin@foo.com.
I20220529-12:09:18.453(-10)?   Creating user john@foo.com.
I20220529-12:09:18.515(-10)? Creating default data.
I20220529-12:09:18.515(-10)?   Adding: Basket (john@foo.com)
I20220529-12:09:18.599(-10)?   Adding: Bicycle (john@foo.com)
I20220529-12:09:18.600(-10)?   Adding: Banana (admin@foo.com)
I20220529-12:09:18.601(-10)?   Adding: Boogie Board (admin@foo.com)
I20220529-12:09:18.773(-10)? Monti APM: completed instrumenting the app
=> Started your app.

=> App running at: http://localhost:3000/
```

Periodically, you might see `Error starting Mongo (2 tries left): Cannot run replSetReconfig because the node is currently updating its configuration` after the `=> Started HMR server.`. It doesn't seem to be a problem since the MongoDB does start.

### Viewing the running app

If all goes well, the template application will appear at [http://localhost:3000](http://localhost:3000).  You can login using the credentials in [settings.development.json](https://github.com/ics-software-engineering/meteor-application-template-react/blob/main/config/settings.development.json), or else register a new account.

### ESLint

You can verify that the code obeys our coding standards by running ESLint over the code in the imports/ directory with:

```
meteor npm run lint
```

## Application Walkthrough

The following sections describe the major features of digits.

#### Landing page

When you retrieve the app at http://localhost:3000, this is what should be displayed:

![](https://github.com/ics-software-engineering/meteor-application-template-react/raw/main/doc/landing-page.png)

The next step is to use the Login menu to either Login to an existing account or register a new account.

#### Login page

Clicking on the Login link, then on the Sign In menu item displays this page:

![](https://github.com/ics-software-engineering/meteor-application-template-react/raw/main/doc/signin-page.png)

#### Register page

Alternatively, clicking on the Login link, then on the Sign Up menu item displays this page:

![](https://github.com/ics-software-engineering/meteor-application-template-react/raw/main/doc/register-page.png)


#### Landing (after Login) page, non-Admin user

Once you log in (either to an existing account or by creating a new one), the navbar changes as follows:

![](https://github.com/ics-software-engineering/meteor-application-template-react/raw/main/doc/landing-after-login-page.png)

You can now add new Stuff documents, and list the Stuff you have created. Note you cannot see any Stuff created by other users.

#### Add Contact page

The Add Contact page allows a user to add a new contact card containing a first name, last name, business address, image URL, and description of their contact.

![](https://raw.githubusercontent.com/johnserraon/digits/cleanup/doc/digits-add-contact.png?token=GHSAT0AAAAAACNAL4U4ITVL3UFCVLS4UYCMZQM6X5Q)

#### List Contacts page

The List Contacts page shows all contact cards that the user has created or has associated with their account.

* Each contact card is equipped with a section to write timestamped notes, helping users keep track of business plans and other miscellaneous contact information.


* You can also click the "Edit" link to go to the Edit Contact page, described next.

#### Edit Contact page

After clicking on the "Edit" link associated with a contact, the details of the card can be edited.

#### Landing (after Login), Admin user

You can define an "admin" user in the settings.json file. This user, after logging in, gets a special entry in the navbar:

![](https://github.com/ics-software-engineering/meteor-application-template-react/raw/main/doc/admin-landing-page.png)

#### Admin page (list all users stuff)

To provide a simple example of a "super power" for Admin users, the Admin page lists all of the Stuff by all of the users:

![](https://github.com/ics-software-engineering/meteor-application-template-react/raw/main/doc/admin-list-stuff-page.png)

Note that non-admin users cannot get to this page, even if they type in the URL by hand.

### Collections

The application implements a single Collection called "Stuffs". Each Stuffs document has the following fields: name, quantity, condition, and username.

The Stuffs collection is defined in [imports/api/stuff/stuff.js](https://github.com/ics-software-engineering/meteor-application-template-react/blob/main/app/imports/api/stuff/stuff.js).

The Stuffs collection is initialized in [imports/startup/server/Mongo.js](https://github.com/ics-software-engineering/meteor-application-template-react/blob/main/app/imports/startup/server/Mongo.js).

### CSS

The application uses the [React implementation of Bootstrap 5](https://react-bootstrap.github.io/). You can adjust the theme by editing the `app/client/style.css` file. To change the theme override the Bootstrap 5 CSS variables.

```css
/* Change bootstrap variable values.
 See https://getbootstrap.com/docs/5.2/customize/css-variables/
 */
body {
  --bs-light-rgb: 236, 236, 236;
}

/* Define custom styles */
.gray-background {
  background-color: var(--bs-gray-200);
  color: var(--bs-dark);
  padding-top: 10px;
  padding-bottom: 20px;
}
```

### Routing

For display and navigation among its four pages, the application uses [React Router](https://reacttraining.com/react-router/).

Routing is defined in [imports/ui/layouts/App.jsx](https://github.com/ics-software-engineering/meteor-application-template-react/blob/main/app/imports/ui/layouts/App.jsx).


### Authentication

For authentication, the application uses the Meteor accounts package.

When the application is run for the first time, a settings file (such as [config/settings.development.json](https://github.com/ics-software-engineering/meteor-application-template-react/blob/main/config/settings.development.json)) should be passed to Meteor. That will lead to a default account being created through the code in [imports/startup/server/accounts.js](https://github.com/ics-software-engineering/meteor-application-template-react/blob/main/app/imports/startup/server/accounts.js).

The application allows users to register and create new accounts at any time.

### Authorization

Only logged in users can manipulate Stuff documents (but any registered user can manipulate any Stuff document, even if they weren't the user that created it.)

### Configuration

The [config](https://github.com/ics-software-engineering/meteor-application-template-react/blob/main/config) directory is intended to hold settings files.  The repository contains one file: [config/settings.development.json](https://github.com/ics-software-engineering/meteor-application-template-react/blob/main/config/settings.development.json).

The [.gitignore](https://github.com/ics-software-engineering/meteor-application-template-react/blob/main/.gitignore) file prevents a file named settings.production.json from being committed to the repository. So, if you are deploying the application, you can put settings in a file named settings.production.json and it will not be committed.

### Quality Assurance

#### ESLint

The application includes a [.eslintrc](https://github.com/ics-software-engineering/meteor-application-template-react/blob/main/app/.eslintrc) file to define the coding style adhered to in this application. You can invoke ESLint from the command line as follows:

```
[~/meteor-application-template-react/app]-> meteor npm run lint

> meteor-application-template-react@ lint /Users/philipjohnson/meteor-application-template-react/app
> eslint --quiet ./imports
```

ESLint should run without generating any errors.

It's significantly easier to do development with ESLint integrated directly into your IDE (such as IntelliJ).

## Screencasts

For more information about this system, please watch one or more of the following screencasts. Note that the current source code might differ slightly from the code in these screencasts, but the changes should be very minor.

  * [Walkthrough of system user interface (6 min)](https://youtu.be/48xu1hrqUi8)
  * [Data and accounts structure and initialization (18 min)](https://youtu.be/HZRjwrVBWp4)
  * [Navigation, routing, pages, components (34 min)](https://youtu.be/XztTdHpv6Jw)
  * [Forms (32 min)](https://youtu.be/8FyWR3gUGCM)
  * [Authorization, authentication, and roles (12 min)](https://youtu.be/9HX5vuXTlvA)
