Build the Blog Post List Component
==================================

Now that we’ve migrated all our content over to Markdown, it’s time for us to learn how to query those Markdown files and start using them within our app. Currently, our `/pages/index.vue` is manually generating all the HTML needed to render a list of blog posts inside of `/components/BlogPostList.vue`, but this is clearly not sustainable and we’d like to programmatically do so.

How do we make this happen? Let’s dive right in!

Setting up asyncData
--------------------

Inside of our script block, the first thing we’re going to do is use Nuxt’s `useAsyncData` function in order to tell Nuxt that we are going to grab content that needs to be fetched from somewhere and will not be immediately available.

The `useAsyncData` function takes two parameters:

1.  The name of the data fetch we want to do
2.  A function to that will tell what kind of data we want to return

Since we’re fetching a list of blog posts, it seems appropriate to call it `blogPostList`. And we’ll define an empty arrow function for now.

📄 **components/BlogPostList.vue**

    <script setup>
    const { data } = useAsyncData('blogPostList', () => {})
    </script>
    

You can learn more about `useAsyncData` in the [official docs](https://v3.nuxtjs.org/api/composables/use-async-data/).

Introducing queryContent
------------------------

When we want to query content, the Nuxt Content module automatically provides a function aptly named `queryContent`. This function takes a single parameter: where you want to query content from. This is a string that will be a path that’s relative to the `content` directory that we created.

In our case, we want to specify a folder just to optimize performance especially since we’ve already sectioned off our blog content. So all we need to do is pass in the relative path as follows:

📄 **components/BlogPostList.vue**

    <script setup>
    const { data } = useAsyncData('blogPostList', () => {
      return queryContent('/blog')
    })
    </script>
    

Once you’ve defined the folder that you want `queryContent` to look into, we then need to tell Nuxt Content what we want to do. In our case, since we want to look for all the content within this folder, we call the function `find`.

📄 **components/BlogPostList.vue**

    <script setup>
    const { data } = useAsyncData('blogPostList', () => {
      return queryContent('/blog').find()
    })
    </script>
    

Now, we’re almost ready to use the data we’re returning. However, before we move on, I’m personally not a fan of the generic name `data` that we’re destructuring. So let’s go ahead and rename that variable to something that’s easily recognizable:

📄 **components/BlogPostList.vue**

    <script setup>
    const { data: blogPostList } = useAsyncData('blogPostList', () => {
      return queryContent('/blog').find()
    })
    </script>
    

### What does queryContent return?

Now that we have our data, you can go ahead and inspect it by rendering it out to the page with something like:

📄 **components/BlogPostList.vue**

    <script setup>
    const { data: blogPostList } = useAsyncData('blogPostList', () => {
      return queryContent('/blog').find()
    })
    </script>
    
    <template>
      <pre>{{ blogPostList }}</pre>
    </template>
    

When you do so, you should see an array that’s filled with data rich objects of all of our blog posts! If you look, you’ll see that Nuxt automatically parses the data from the Markdown file like:

*   `title`
*   `path`
*   `description`
*   And much, much more!

![Preview of the data structure that Nuxt Content can return](https://firebasestorage.googleapis.com/v0/b/vue-mastery.appspot.com/o/flamelink%2Fmedia%2F05-01.jpg?alt=media&token=12783341-78f2-4580-b033-e8cafd4252ec)

This is really exciting because with just this query, we can now do a lot of interesting things with it. So let’s go in and actually use it in our component!

Using data from Nuxt Content
----------------------------

Inside of our app, all we need to do now is replace the static content with the different properties available to us. Things we’ll need to swap out include:

*   Using `v-for` on our `<div class="card article">` to render the blog posts
*   The blog post title with `blogPost.title`
*   The blog post author with `blogPost.author`
*   The blog post publish date with `blogPost.dates.published`

And with that, here’s the final result:

📄 **/components/BlogPostList.vue**

    <script setup>
    const { data: blogPostList } = useAsyncData('blogPostList', () => {
      return queryContent('/blog').find()
    })
    </script>
    
    <template>
      <div class="container">
        <section class="articles">
          <div class="column is-8 is-offset-2">
            <div
              v-for="blogPost in blogPostList"
              :key="blogPost._path"
              class="card article"
            >
              <NuxtLink to="/blog/my-second-blog-post">
                <section class="blog-post-card card article">
                  <div class="media">
                    <div class="media-content has-text-centered">
                      <h3 class="title article-title has-text-weight-bold">
                        {{ blogPost.title }}
                      </h3>
                      <BlogPostMeta
                        :author="blogPost.author"
                        :date="blogPost.dates.published"
                      />
                    </div>
                  </div>
                  <div class="card-content">
                    <div class="content article-body is-size-5">
                      {{ blogPost.description }}
                    </div>
                  </div>
                </section>
              </NuxtLink>
            </div>
          </div>
        </section>
      </div>
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
    

And just like that it, everything shows up like magic! The possibilities you get out of this with just being able to manage everything locally, have it version controlled, and then you can just query it and spit it out is absolutely incredible.

Let’s ReVue
-----------

In this lesson, we’ve learned how to query content with Nuxt Content v2 using the `queryContent` function so that the data can be utilized within our app!

That said, we’re not quite out of the woods yet. We’ve still got learn how to render our full body content onto the page while actually generating page routes for it, which is what we’ll do in the next lesson.

### Lesson Resources

##### Source Code:

*   [Starting Code](https://github.com/Code-Pop/build-a-blog-with-nuxt-3-and-nuxt-content-v2/tree/05-begin)
    
*   [Ending Code](https://github.com/Code-Pop/build-a-blog-with-nuxt-3-and-nuxt-content-v2/tree/05-end)
