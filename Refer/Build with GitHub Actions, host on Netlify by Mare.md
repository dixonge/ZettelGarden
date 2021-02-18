# Build with GitHub Actions, host on Netlify | by Marek Pukaj | Medium

[https://medium.com/@MarekPukaj/build-with-github-actions-host-on-netlify-ebf5fa505616](https://medium.com/@MarekPukaj/build-with-github-actions-host-on-netlify-ebf5fa505616)

[[Build%20with%20GitHub%20Actions,%20host%20on%20Netlify%20by%20Mare%204b50396e0fc64629acf3beb457bcbc57 0XblV3Q0JVGIpHCRl]]

Photo by [EJ Yao](https://unsplash.com/@hojipago?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

As a software developer, you probably don’t just write code. Sometimes you have to do a lot of supportive tasks whether you like it or not.

One of these tasks is definitely building CI/CD process. This can be really challenging, especially when you have to deal with the deployment to multiple environments. Whether it is development, staging or production environment, you want to host them usually from the same repository, but on the separate URLs, using different environment variables.

When you want to build this deployment setup using Netlify as a service for hosting your builds, you have to create a separate site for each environment and link them with the same repository. Then if you want to serve different content for each environment, you can set up which branch you want to use for which site. The problem is, that with the new Netlify pricing policy, you have just **300 build minutes per month** in the free plan. And that might not be enough. When you want to have multiple environments within the same Netlify account, your 300 free minutes can be drained out really fast. With Netlify you are also very limited in what you can do in your build process. So how can we optimize this setup?

# GitHub Actions save the day

One possible solution is to move the build process from Netlify to GitHub Actions. Asking what’s the difference? With GitHub Actions, you have **2 000 free build minutes per month**, which is nearly **7 times** more than with Netlify. On top of this, you get more flexibility when creating your CI/CD workflow. Wanna try it? Let’s jump into it and create our solution for the integration of these two services into one CI/CD process.

# Setup Netlify

Before we start building our CI/CD workflow, we need to create Netlify sites for our environments. In this example, we are going to use three of them. Development, Staging, and Production. When creating the sites for these environments, **the important thing is to not create them from the git repository**. Instead, we have to create our sites without connecting them to git. To do so we have to use drag and drop field at the bottom of a Netlify sites list. We can drop an empty folder to this field if we want to create a disconnected site. I know that this solution is kind of hacky, but currently, I don’t think that there is some more elegant way of doing this. Hopefully, the Netlify team will provide us a better solution for this case in the future.

# Integrate GitHub Actions with Netlify

Now, that we have our Netlify setup done, we can move on to the actual CI/CD workflow. In this section, I assume that you have at least a basic understanding of GitHub Actions. If not, please refer to the official [GitHub Actions documentation](https://help.github.com/en/actions).

Let’s create an example situation. Let’s say we have a repository with the two main branches `master` and `dev`. Every time we push code to the `dev`, we want to deploy the content of this branch to our development environment on Netlify. Our first workflow might look like this.

deployment.yml

This workflow file contains the definition of our deploy job. As you can see from lines 3 to 6, we run this job on every push to the `dev` branch. This is exactly what we want.

Now let’s look at our deploy job and specifically on the step called `Deploy to Netlify`*.* In this step, we are using [official Netlify CLI action](https://github.com/netlify/actions/tree/master/cli), which allows as to run Netlify CLI directly from our workflow. As you want to deploy our site, we are using *deploy* command with *dir* and prod *flags*. We also need to provide CLI two secrets `NETLIFY_AUTH_TOKEN` and `NETLIFY_SITE_ID` .

To get `NETLIFY_AUTH_TOKEN` value, we have to open our Netlify account, navigate to **User settings -> Applications -> Personal access tokens** and then by clicking on the button we generate our token for our GitHub Actions workflow.

To get `NETLIFY_SITE_ID` we need to open our Netlify site, that we created for a development environment. Then we open **Settings** and under **Site information,** there is **API ID** which will be our `NETLIFY_SITE_ID` value.

As you can see we don’t expose our secret values directly to the workflow file. Instead, we use the GitHub build-in way of storing secrets that will be exposed only to selected actions. You can set secrets for your repository by going to **Setting -> Secrets**. These secrets can be used also for other environmental variables that you need in your build process.

## Run tests before merging

Now we have our development workflow. Let’s extend our example a little bit further. We want to run our tests for every pull request to the `master` branch. Here is our code for our next workflow.

test.yml

This code contains a description of the test workflow. In this example, we test our application using Cypress. To run Cypress within our workflow we use official Cypress action for running our tests.FF

## Protect our branch

Running tests before merging code to the `master` is a good practice, but currently, we can still merge our pull request even if our tests are failing. To fix this issue we need to protect our `master` branch by requiring status checks to pass before merging. To do so, in your repository navigate to **Settings -> Branches -> Branch protection rules** and click **Add rule.** Then check to **Require status checks to pass before merging,** find the name of your job, which is in our case called `test` and check it. From now on you will be able to merge pull requests only if your tests are passing.

## Deploy to the staging

So far so good. Let’s move further and prepare deployment workflow for our staging environment. In our example process, we want our staging environment to reflect our `master` branch. We want a staging environment to be as close as possible to the production environment. Therefore we are going to create a workflow, that will deploy our build to the staging environment for every push to the `master` .

staging.yml

We can see, that this workflow is very similar to the workflow that we use for development environment deployment. The only difference is in the branch that we deploy.

## Deploy to the production

To finish our journey we must create our last workflow for deployment to the production. In our case, we are going to deploy our code to the production by tagging our commit with a tag name containing `v` . This will be our release tag. We can label the last commit in `master` right from GitHub by going to the **releases** tab and then clicking on a **Create new release** button. Now, finally, we can create a last workflow file.

production.yml

There is not much new going on here in this file. The only one import thing here is on lines 3 to 6. On these lines, we specify, that we want to run our workflow just for commits tagged with `v` in the name. And here we are. That was our final step in our CI/CD process.

# Summary

We covered a lot in this tutorial. We created a CI/CD process that integrates together two very popular services. We are now able to automatically test our code and deploy it to the various environments. There are many approaches to this problem, but I wanted to show one specific solution. Thank you for reading this. I hope you learned something new! If you have your own way of doing this or if you know about any improvements to this process, please let me know in the comments.