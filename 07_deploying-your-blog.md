Deploying Your Blog
===================

Now that you have a working blog that uses Markdown and Vue components to display amazing content, it’s time for the next step: deploying your project so that other people can see everything you’ve built!

Setting up your project for deployment
--------------------------------------

There are lots of sites that offer free services for deploying your site, but today I’ll be showing you how to use Netlify, one of the most popular services for managing site deployments and making developer’s life much easier when it comes to distributing their sites and/or applications around the world.

If you don’t have one already, you can get a free account by signing up here: [https://app.netlify.com/signup](https://app.netlify.com/signup). Once you’ve signed up and authenticated with GitHub, you should be able to follow these instructions.

### Creating a new site on Netlify

Once you login to your account, you’ll want to click on the button to “Add a new site” which you’ll see on the main dashboard. You’ll then get a dropdown menu where you’ll want to click on “Import an existing project.” Here’s what mine looks like:

![Preview of a Netlify dashboard and what the add new site dropdown menu looks like](https://firebasestorage.googleapis.com/v0/b/vue-mastery.appspot.com/o/flamelink%2Fmedia%2F07-01.jpg?alt=media&token=da6d92be-a2c9-4e24-a4ed-2978a9bc72ef)

What’s great about this workflow is that you’ll get to import your project directly from GitHub which is going to enable some really powerful features we’ll talk about later on in this course.

Assuming you have all the permissions set up correctly, you’ll eventually come upon this screen to configure everything.

![Preview of the configuration page on Netlify for deploying a Nuxt 3 app](https://firebasestorage.googleapis.com/v0/b/vue-mastery.appspot.com/o/flamelink%2Fmedia%2F07-02.jpg?alt=media&token=2d9fce89-86c4-42ad-b65d-807ba3f64a7b)

By default, Netlify should detect most of the configurations you need; but in case it doesn’t, you’re basically setting up what scripts should be run automatically for each deploy.

*   **Base Directory:** Left blank since it will automatically assume the root folder
*   **Build Command**: `npm run build` as you would probably expect
*   **Publish Directory**: `dist` which is the default folder when a Nuxt project is built

Once all the fields are filled out correctly, it’s time to click “Deploy site” and the robots will be off to the races to deploy our site! Once everything is done running, you should see a custom URL that Netlify automatically generates for you ([which you can configure yourself whenever you want](https://answers.netlify.com/t/meaning-behind-netlify-subdomains/3838)).

![Preview of the deployed blog site would look like](https://firebasestorage.googleapis.com/v0/b/vue-mastery.appspot.com/o/flamelink%2Fmedia%2F07-03.jpg?alt=media&token=6c42ab39-50ce-437b-809b-7d4803173b3d)

But what if you want to make changes?
-------------------------------------

Now that your site is deployed, you might be wondering what happens when you need to make a change. After all, most sites are always in need of updates and changes. Well, even though you might not be aware of it yet, you’re already set up for success!

Remember how we connected created a new site on Netlify by connecting it to the GitHub repo? Well guess what? That means that Netlify will automatically watch your repo and deploy new sites whenever you want to make a change. This is also know as CI/CD (i.e., continuous integration / continuous deployment). In other words, what this means is that anytime you make any changes to the code, it’ll manage all of the deployment for you so that you don’t have to worry about caching, and more.

While it might not seem like a big deal at first, this really helps to upscale the developer workflow because you can focus on doing what you do best, which is pushing code. Rather than worrying about making sure that the users are getting exactly what you deliver via server or CDNs, you can just build the best thing you possibly can.

We can demonstrate this by updating our code to update the counter to increment by two instead of one. Once we commit this code and push it, you’ll see in the Deploy section of the site that a new deploy has been kicked off.

![Preview of what the deploy list looks like within the Netlify deploy dashboard](https://firebasestorage.googleapis.com/v0/b/vue-mastery.appspot.com/o/flamelink%2Fmedia%2F07-04.jpg?alt=media&token=fd143f81-6053-4601-bf48-cc06a812f280)

Once it’s finished, you’ll notice that the deployed site now contains the updated code. That easy!

And while it might seem like just another line item, this comes to the next benefit: atomic deploys.

The power of atomic deploys
---------------------------

Atomic deploys essentially mean that each deploy lives entirely on its own. No dependencies on one another and they exist in isolated contexts. And when Netlify creates a deploy of your site, **every deploy is an atomic deploy**. As a result of this approach, this means that you can switch between different deploys of your sites with just a couple of clicks.

To illustrate just how powerful this is, let’s assume that you’ve been told that the counter change we implemented for incrementing by two is causing a lot of issues. And while a simplistic example, this is common when people need to roll back changes that were made.

Without atomic deploys, this would often require a significant amount of work in terms of:

1.  Reverting the changes in GitHub
2.  Redeploying the site
3.  Trying to invalidate the cache so that users aren’t served an old version of the site
4.  And so forth

But with atomic deploys, it’s as simple as telling Netlify to serve an older version of you site instead of a new one by clicking around the UI. And the best part? The change is practically instant and users will all get the right version when they load the site.

And while we’ve just scratched the surface of things that Netlify can do to make your life easier as a developer, you’re now fully capable of deploying your projects and sharing them with the rest of the world.

Let’s ReVue
-----------

In this lesson, we learned how to:

*   Setup a project on Netlify to deploy your site for free
*   Leverage automatic deployments whenever you push changes to your main branch
*   Use atomic deploys to ensure that users get the same deployments while making it easy to rollback when needed

And the best part about this is that you can apply these basic principles to other projects as well. Happy deploying!

