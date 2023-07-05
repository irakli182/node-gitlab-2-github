# Explanation of migration proccess from gitlab to github step by step.

## step 1 - Importing branches from gitlab.

Importing main repositroy with branches from gitlab to github is relatively simple. 
It consists of few steps:

1. Create new repositroy on github
2. Click ```import repository```
3. Write old projects URL into ```Your old repository's clone URL``` field
4. Begin import

NOTE: If repository is private, github will redirect to login page. In the username field enter your login, and in the password field enter gitlab's personal token.

With those steps repository is imported from gitlab to github with all branches.

## step 2 - importing issues, pull requests, milestones etc.

While github allows us to directly import repository from gitlab, issues, milestones, pull requests etc. are not imported.
To address following issue, [special third-party tool](https://github.com/piceaTech/node-gitlab-2-github) will come handy. 

Setting up the tool is relatively simple: you have to generate tokens on both, github and gitlab, get repository names etc. detailed information [here](https://github.com/piceaTech/node-gitlab-2-github/blob/master/README.md)

However, the tool has tricky and confusing parts:

1. Setting up `sessionCookie`.
   - Gitlab has special [part](https://gitlab.com/-/profile/active_sessions) where sessions are listed. This IS NOT what you need.
   - To get proper sessionCookie:
       - go to inpect element using `f12`
       - press `application`
       - press `cookies`
       - search for `_gitlab_session` and copy it's value

2. Setting up ```AWS s3``` for attachments 
   - To migrate attachemnts, AWS s3 bucket is neccessary as a third-party tool.
   - steps:
       - Create AWS IAM user with `read and write` permissions, and get it's security credentails. 
       - Create AWS s3 bucket. Bucket has to be public, otherwise it won't be accessable from github.
       - After these steps everything should work fine, attachemnts will be migrated and accessable.
    
### notes

[issues, milestones, attachments and pull requests migration tool](https://github.com/piceaTech/node-gitlab-2-github)
