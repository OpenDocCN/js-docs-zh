# Userguides

# Sails.js User Guides

### Guides

> This will be a top level documentation section on the sails.js website as soon as we get a little more content for it.

Sails.js was created by the Balderdash team out of necessity in order to quickly and efficiently make rock solid apps for our clients. We then open sourced it so others could do the same. Client work is still what pays the bills at Balderdash and while we love to work on Sails full time, we just can't. This section is part of an ongoing effort to further open up the Sails.js framework to the community and keep Balderdash from constraining it's growth.

#### How can you help?

Think about how you have used Sails for your project then write a guide about it!

#### What should I write about?

*   If you have a less than common use case, write a guide about it.
*   If you had a hard time finding a solution to a particular problem while using Sails, write a guide describing your workaround.
*   Are you doing something unconventional with Sails? Write a guide.
*   Are you using Sails for your embedded hardware project? Please, for the love of God, write a guide!

#### Okay, I'll do it! Now what?

Thanks. You're awesome! Now, before you write anything, see the very first user guide in this folder under [contributing.md](https://github.com/balderdashy/sails-docs/blob/master/userguides/contributing.md)

#### Legal Disclaimer

Just kidding about the legal disclaimer. Seriously though, thank you for contibuting. If it weren't for the help of folks like you, this project wouldn't be half of what it is today. You guys rock.

#### Sincerely and Truly

Nick (@uncletammy)

<docmeta value="sailsUserGuides83838" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="User Submitted Guides" name="displayName" class="calibre17"></docmeta>

# Contributing

### Submit Your Own Guide

Submitting your own guide is easy. Read this guide in its entirety before submitting a PR though.

### Sails.js Documentation Structure

The documentation on the Sails.js website is automatically pulled down from the `sails-docs` github repo and all of the .md files which contain github flavored markdown are turned in html templates. Every time the `sails-docs` repo changes, the changes are instantly reflected on the website.

In order for this to work, the sails-docs repo must have a particular structure. It's easy to follow though.

##### The Basics

Every folder must contain a .md file with the same (case sensitive) name. A folder called `SecuRity` must contain `SecuRity.md`. This file will be loaded when someone clicks the link on the guides navigation menu.

Every .md file must contain two `<docmeta>` tags. They are required for automatically generating the navigation. Without these tags, the template is ignored.

The `uniqueID` tag is used by the router on the front-end of the Sails.js website. The value can be anything as it's unique among all the other .md files. We add some random numbers to it just in case.

```
<docmeta name="uniqueID" value="someUniqueName85732"> 
```

The value of the `displayName` tag determines the link text on the navigation menu. This does not need to be unique.

```
<docmeta name="displayName" value="Name To Appear On Navigation"> 
```

##### Making a New Section

Lets say you want to create a guide called `Socket.io Safety` in a new section called `Security`.

*   First, create the folder `sails-docs/userguides/security/`
*   Next, create the file `sails-docs/userguides/security/security.md`
*   Add your introduction/overview of the section to security.md and make sure to include your `<docmeta>` tags
*   Now, create `sails-docs/userguides/security/socketio.md` and put the content for your guide in it. Make sure to include `<docmeta>` tags

If there is already an appropriate section for your guide, skip to the last step.

##### The `Contributed By` section.

This section is entirely optional. Feel free to use it to talk a little about yourself.

#### Example Stub

Feel free to copy and change the file `guideStub.md`

### Contributed By

##### Nicholas Crumrine

A real West Texas cowboy with an affinity for cats

##### Link

[`twitter.com/ncrumrine`](https://twitter.com/ncrumrine)

##### Organizations

Sails, Balderdash,cluckus

<docmeta value="sailsUserGuidesContributing80998" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="Submit A Guide" name="displayName" class="calibre17"></docmeta>

# Deployment

### Deploying your app

Make sure you see 'before deployment' guide in 'security'

### Picking a host

Here are some hosts...

<docmeta value="guidesDeployment87563" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="Deployment" name="displayName" class="calibre17"></docmeta>

# Nodejitsu

### Deploying to Nodejitsu

### This guide was brought to you by

##### Name

##### Bio

##### Link

##### Organization

##### Etc...

<docmeta value="guidesDeploymentNodjitsu402941" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="Nodejitsu" name="displayName" class="calibre17"></docmeta>

# Openshift

### Deploying to OpenShift

### This guide was brought to you by

##### Name

##### Bio

##### Link

##### Organization

##### Etc...

<docmeta value="guidesDeploymentOpenshift407333" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="Openshift" name="displayName" class="calibre17"></docmeta>

# Guide Stub

# Document Stubb

### This is a stub!

Here is some information

### Contributed By

##### Name

##### Bio

##### Link

##### Organization

##### Etc...

<docmeta value="littleStubFriend19283" name="uniqueID" class="calibre25"></docmeta>

<docmeta value="someName" name="displayName" class="calibre17"></docmeta>