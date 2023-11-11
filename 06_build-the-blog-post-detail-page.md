Build the Blog Post Detail Page
===============================

Now that we know how to manage content and query that content with Nuxt Content, it’s time for us to learn how to render the blog post in its entirety. After all, for anyone who’s tried to do this from scratch before, building a rendering engine for Markdown is no small accomplishment!

Generating dynamic routes
-------------------------

Before we render out each blog post though, we’ll also need to ensure that Nuxt is generating routes for all of our content so that we don’t have to manually manage this.

In order to do this, we’ll leverage the dynamic file naming pattern which leverages the square brackets and triple periods to tell Nuxt that this is something dynamic.

    .
    └── pages
    │   └── blog
    │       └── [...slug].vue
    

The reason we have it configured like this is because the desired blog URL most people are used to is something like: `www.mysite.com/blog/title-of-blog-post`.

Inside of our newly created file, let’s scaffold the core structure of what the blog post detail page will look like:

📄 **/pages/blog/\[…slug.vue\]**

    <script setup>
    </script>
    
    <template>
      <main>
        <TheHero>
          <template v-slot:default>
            <!-- Blog title goes here -->
          </template>
    
          <template v-slot:subtitle>
            <BlogPostMeta
              author=""
              date=""
              color="dark"
            />
          </template>
        </TheHero>
        <div class="container">
          <section class="articles">
            <div class="column is-8 is-offset-2">
              <section class="blog-post-card card article">
                <div class="card-content">
                  <div class="content article-body is-size-5">
                    <!-- Blog content goes here -->
                  </div>
                </div>
              </section>
            </div>
          </section>
        </div>
      </main>
    </template>
    

Querying one piece of content
-----------------------------

In the last lesson, we queried every content available in the `blog` directory because we needed a list. However, in this page, we only need one piece of content. How will we accomplish that?

Let’s start by setting up our function similar to before:

📄 **/pages/blog/\[…slug.vue\]**

    <script setup>
    const { data: blogPost } = await useAsyncData(`content`, () => {
      return queryContent()
    })
    </script>
    

At this point, we have a problem, which is the fact that we need a unique identifier that will allow us to ensure we’re fetching content for this specific page. And since URLs should be unique, the dynamic slug is a great solution for this. We can utilize the `useRoute` function in order to fetch the `path` property. Once we do that, we can append that to the name of our `useAsyncData` function for a unique query name.

📄 **/pages/blog/\[…slug.vue\]**

    <script setup>
    const { path } = useRoute()
    
    const { data: blogPost } = await useAsyncData(`content-${path}`, () => {
      return queryContent()
    })
    </script>
    

Now it’s time for us to learn about a new method called `where` which will allow us to essentially filter content based on certain conditions. Here’s how it looks in action:

📄 **/pages/blog/\[…slug.vue\]**

    <script setup>
    const { path } = useRoute()
    
    const { data: blogPost } = await useAsyncData(`content-${path}`, () => {
      return queryContent().where({ _path: path })
    })
    </script>
    

Where invoking `where`, it takes an object that contains the parameters you want to match. In this page, we want to only look for files where the `_path` property matches the actual `path` of the page. And since we’ve structured the content directory to already use the `/blog` convention, this will work perfectly!

Finally, before we can move on, rather than using `find` like we did in the last lesson, we will be using `findOne` instead which only returns one result.

📄 **/pages/blog/\[…slug.vue\]**

    <script setup>
    const { path } = useRoute()
    
    const { data: blogPost } = await useAsyncData(`content-${path}`, () => {
      return queryContent().where({ _path: path }).findOne()
    })
    </script>
    

Rendering the content on the page
---------------------------------

For most Markdown rendering libraries, this is the point of the blog post where we would have to dive into how to parse the Markdown from our blog posts and render it. However, this is Nuxt Content we’re talking about, and the Nuxt team never ceases to amaze when it comes to developer experience.

Believe it or not, Nuxt Content provides a built-in component called `ContentDoc` which takes care of everything by default! 🤩

Once everything is put together, you should have the following component:

📄 **/pages/blog/\[…slug.vue\]**

    <script setup>
    const { path } = useRoute()
    
    const { data: blogPost } = await useAsyncData(`content-${path}`, () => {
      return queryContent().where({ _path: path }).findOne()
    })
    </script>
    
    <template>
      <main>
        <TheHero>
          <template v-slot:default>{{ blogPost.title }}</template>
    
          <template v-slot:subtitle>
            <BlogPostMeta
              :author="blogPost.author"
              :date="blogPost.dates.published"
              color="dark"
            />
          </template>
        </TheHero>
        <div class="container">
          <section class="articles">
            <div class="column is-8 is-offset-2">
              <section class="blog-post-card card article">
                <div class="card-content">
                  <div class="content article-body is-size-5">
                    <ContentDoc />
                  </div>
                </div>
              </section>
            </div>
          </section>
        </div>
      </main>
    </template>
    
    <style>
    .blog-post-card {
      padding-top: 2.5rem;
      padding-bottom: 3rem;
    }
    
    .blog-post-card .card-content {
      padding: 1rem;
    }
    
    .blog-post-card .title {
      margin-bottom: 1rem;
    }
    </style>
    

For more info, check out the [official docs on rendering content with Nuxt Content](https://content.nuxtjs.org/guide/displaying/rendering).

What about code syntax highlighting?
------------------------------------

When you look at the page, you might notice that the code syntax highlighting is not working by default. And this is expected because not everyone will use this feature. However, since we’re developers, I figured it was worth devoting a section to this since it’s likely we’ll be sharing some sort of code snippet at some point.

To configure this, we need to go into our `nuxt.config.ts` file and tell the Nuxt Content module that we want to use syntax highlighting. The way we do this is by configuring the theme we want to use. In my case, I’ll use the standard `github-light`.

📄 **nuxt.config.ts**

    import { defineNuxtConfig } from 'nuxt'
    
    export default defineNuxtConfig({
      modules: ['@nuxt/content'],
      content: {
        highlight: {
          theme: 'github-light'
        }
      }
    })
    

Once that’s configured, you can restart your server and everything should work as expected!

![Preview of what code syntax highlighting can look like](https://firebasestorage.googleapis.com/v0/b/vue-mastery.appspot.com/o/flamelink%2Fmedia%2F06-01.jpg?alt=media&token=72872ba7-bb94-4e1c-9eaa-b63b22c01d47)

You can learn more about syntax highlighting themes from the [Shiki docs](https://github.com/shikijs/shiki).

Let’s ReVue
-----------

In this lesson, you’ve learned:

*   How to generate a dynamic page that leverages Nuxt Content
*   How to render content
*   How to configure syntax highlighting

With that, it’s time for us to learn how to deploy our app and share it with the rest of the world. See you in the next lesson!

### Lesson Resources

##### Source Code:

*   [Starting Code](https://github.com/Code-Pop/build-a-blog-with-nuxt-3-and-nuxt-content-v2/tree/06-begin)
    
*   [Ending Code](https://github.com/Code-Pop/build-a-blog-with-nuxt-3-and-nuxt-content-v2/tree/06-end)
