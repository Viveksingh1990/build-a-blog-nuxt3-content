Project Overview and Setup
==========================

In this lesson, we’ll be taking a look at the project you’ll be building and setting up Nuxt Content. Let’s get started!

Features
--------

In this course, we’ll be building a blog with a standard layout using Bulma which has a:

*   Top navigation bar
*   Title / Hero area
*   List of blog posts
*   Blog detail page to read the blog post in its entirety

How Resources are Imported
--------------------------

You might be wondering how all these assets are being imported. To see how this works, let’s jump into `app.vue`.

Inside of the `<script>` block, you’ll see that there is a new method introduced in Nuxt 3 called `useHead`.

    useHead({
      title: 'Nuxt 3 Bulma Blog Template',
      link: [
        {
          rel: 'stylesheet',
          href: '<https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css>'
        },
        {
          rel: 'stylesheet',
          href: '<https://cdnjs.cloudflare.com/ajax/libs/overlayscrollbars/1.9.1/css/OverlayScrollbars.min.css>'
        },
        {
          rel: 'stylesheet',
          href: '<https://fonts.googleapis.com/css?family=Open+Sans>'
        },
        {
          rel: 'stylesheet',
          href: '<https://unpkg.com/bulma@0.9.3/css/bulma.min.css>'
        }
      ]
    })
    

This method allows you to inject resources into the `<head>` tags on a page. As you can see in this list, this is where all the fonts and CSS files are being imported.

This is incredibly powerful because it allows you to dynamically import resources as needed depending on what the client needs. In this particular case, since we added this in `app.vue`, it will be imported on every page since it’s the root component.

Project Structure
-----------------

The project was scaffolded using the [Nuxi](https://www.npmjs.com/package/nuxi) and follows a standard Nuxt 3 template.

If you’d like to learn more about Nuxt 3 fundamentals, be sure to check out our [Nuxt 3 Essentials](https://www.vuemastery.com/courses/nuxt-3-essentials/nuxt-3-overview/) course.

### Routing

It utilizes the page based routing structure so that we don’t have to configure Vue Router ourselves.

    .
    ├── components
    ├── pages
    │   ├── blog
    │   │   ├── my-first-blog-post.vue
    │   │   └── my-second-blog-post.vue
    │   └── index.vue
    ├── app.vue
    ├── nuxt.config.ts
    ├── package.json
    ├── README.md
    └── tsconfig.json
    

For example, `/blog/my-first-blog-post.vue` will be automatically create a route on your site as `/blog/my-first-blog-post`.

And in case you’re wondering whether we’ll be hard-coding all future blog posts in the blog directory, just know this is a starting place. You’ll learn how to generate dynamic routes later on in this course!

### Components

In addition, to give us a place to start, I’ve already built out some components for us to use. Some key ones to note are:

*   **BlogPostList** - Manages the list of cards being displayed on the home page
*   **TheHero** - Provides the standard hero component to display a title and subtitle (as needed)
*   **TheNavbar** - Scaffold the top bar for navigation

We won’t go over how they are built, but the source code is there for you to review if you’d like!

The Blog Post Detail Page
-------------------------

If you open up `pages/blog/my-first-blog-post.vue`, you might notice that the entire content of the page is hard-coded HTML.

    <!-- Small snippet -->
    <template>
      <main>
        <div class="container">
          <section class="articles">
            <div class="column is-8 is-offset-2">
              <section class="blog-post-card card article">
                <div class="card-content">
                  <div class="content article-body is-size-5">
                    <h1 id="sample-markdown">Sample Markdown</h1>
                    <p>This is some basic, sample markdown.</p>
                    <h2 id="second-heading">Second Heading</h2>
                    <ul>
                      <li>
                        Unordered lists, and:
                        <ol>
                          <li>One</li>
                          <li>Two</li>
                          <li>Three</li>
                        </ol>
                      </li>
                      <li>More</li>
                    </ul>
                  </div>
                </div>
              </section>
            </div>
          </section>
        </div>
      </main>
    </template>
    

And while it may seem easy to navigate for those familiar with HTML, anyone who has spent time writing and managing content can tell you how painful it is to do at scale. After all, when you write and edit content, that’s what you want to focus on, and not whether the HTML syntax is valid or not.

Wouldn’t it be nice if we could import Markdown into our project? Well no more wishing needed because Nuxt Content is here to the rescue!

Adding Nuxt Content v2 to Our Project
-------------------------------------

### Installing Nuxt Content v2

To add Nuxt Content v2 to our project, we’ll run:

    npm install --save-dev @nuxt/content
    

Once it’s been installed, you can verify that it’s been installed correctly in our `package.json` file by checking the `devDependencies` section.

    {
      "private": true,
      "scripts": {
        "build": "nuxt build",
        "dev": "nuxt dev",
        "generate": "nuxt generate",
        "preview": "nuxt preview"
      },
      "devDependencies": {
        "@nuxt/content": "^2.0.1",
        "nuxt": "^3.0.0-rc.3"
      }
    }
    

### Configuring Nuxt Content v2

Before we can use Nuxt Content v2, we need to tell Nuxt 3 that we want to use it. And the way we do this is configuring it inside of `nuxt.config.ts`.

For those worried about the `.ts` extension, don’t worry, no TypeScript knowledge is needed at all for this next step.

To do this, you’ll add a `modules` config option to the Nuxt config that takes an array of strings (which correspond to the modules you want to use).

    import { defineNuxtConfig } from 'nuxt'
    
    export default defineNuxtConfig({
      modules: ['@nuxt/content']
    })
    

As you can see in our config, we add in our `@nuxt/content` module as a string. And that’s all the configuration you need to do!

Let’s ReVue
-----------

In this lesson, we took a look at how the project is structured for this course and how you can add Nuxt Content v2 to a Nuxt 3 app. And just like that, we’re ready for the next steps of our course. See you in the next lesson!

### Lesson Resources

##### Source Code:

*   [Starting Code](https://github.com/Code-Pop/build-a-blog-with-nuxt-3-and-nuxt-content-v2/tree/02-begin)
    
*   [Ending Code](https://github.com/Code-Pop/build-a-blog-with-nuxt-3-and-nuxt-content-v2/tree/02-end)
