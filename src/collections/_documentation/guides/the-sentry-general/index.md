---
title: The Sentry General
sidebar_order: 7
---

Have you ever...?
"How do large enterprise organizations uses Sentry?"
"I did the basics, but What's next? Recommendations? Best Practices?

You'll see Basic and Advanced. If you have the Basics down, then try Advanced!

## Architecture
Organization > Teams > Projects 

Organization - You only need 1. It has many teams.

Team - A Team has many Projects in a one-to-many relation. 

Get your User added to a Team in order to access the Team's Projects. https://docs.sentry.io/accounts/membership/#restricting-access. 

Roles(link)Project -  An entity in Sentry representing one of your apps. It receives the errors that the Sentry DSK installation captures in your app.
[picture]

#### Monoliths, Microservices, Repositories | How Many Projects Should I create?

Basic - The recommended way for both small and large enterprises to represent each of their apps in Sentry is with their own Project in Sentry.

If your monolithic app has multiple code bases, then create a Project for each of those.

If your monolithic app is 1 code base but runs discreetly in different ways (e.g. one instance of it powers the API, and another instance powers marketing pages), then create a Project for each instance.

(Alerts + Issue Owners can be configured based on subdirectories in your source code to route errors to the appropriate teams).

If you have multiple back-end microservices, then create a Project for each of those microservices.

Advanced - If you have multiple dev teams working on 1 monolithic app, then configure your Alerts & Issue Owners based on the 'file path' that the error is coming from. This way, errors from ./src/* notify the 1 team who manages src/* while errors from something else like ./middleware/* go to the team that manages the middlewares. Order of precedence, so if you specify a fallback condition of ./*

https://docs.sentry.io/guides/getting-started/#-how-many-projects-should-i-create  
https://docs.sentry.io/error-reporting/quickstart/?platform=python#configure-the-sdk  
https://docs.sentry.io/error-reporting/configuration/?platform=python#dsn  
(key vocab - dsn)

Teams - [Open Membership](https://docs.sentry.io/accounts/membership/#open-membership) allows members to manage their own teams, without an admin.

#### Releases(?)
definitions
Release - a version of your code that is deployed to an environment. (It can correlate with a deployment of your app but doesn't have to)

sentry-cli - basicReleases let you track which errors came from which releaseReleases have commits associated to them, so you can tell which commits may [suspect commits](link) behind the errors

You can make the Release # based on an environment variable that is set during your build process.  
You can make the Release # by using sentry-cli, which will generate a new release # if there have been new commits since the previous release. 

Sentry-cli will verify commit info in the .git subdirectory (or via the integration?) as well as Release numbers via Sentry.io.

advanced  
Can keep release # in one-to-one correlation to your app's version (think Release in Github). If you trigger a build (and new sentry Release) on every commit in your CI/CD but only some of these get deployed to Production, that's okay because you'll be able to track the Releases in Sentry specifically from Production. 

When you deploy a new release, you can specify the commits yourself if you don't want sentry-cli to do this for you. Cross-repo commits would allow you to tell that it is coupled to N projects.



## Define Your Data
## Filtering
## Sensitive Data
## Workflow & Integrations
## Understanding Your Volume
## Hosted vs Self-Hosted