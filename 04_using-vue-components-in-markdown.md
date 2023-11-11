Using Vue Components in Markdown
================================

With that first blog post successfully converted, it’s time to convert the second one. However, we have a new challenge when it comes to writing the Markdown. In the past, Markdown always had an inherent limitation in that it assumed everything would be in simplistic text or code. What happened if you wanted something more dynamic? That’s what we’re here to talk about this lesson.

The limitations of Markdown
---------------------------

When we take a look at the blog post when rendered on the page, you’ll notice that there is a live counter which users can interact with.

And while this is fairly straightforward to do within Vue itself, it leaves us a bit puzzled because there is no reactivity system or Vue when we migrate this over to Markdown.

So the question is, how do we solve this? Wouldn’t it be nice if we could just add a Vue component to Markdown directly? Well, if you thought that, you’re just in luck, because Nuxt Content can help bring your Markdown files to a whole new level.

Using what we learned in the last lesson, let’s go ahead and migrate all the content over. This is a short blog post, so the conversion consists primarily of:

*   Frontmatter title to define a title that’s different from the file title
*   H2 heading
*   Paragraph element

📄 **/content/blog/my-second-blog-post.md**

    ---
    title: What is a counter?
    ---
    
    ## What is a counter?
    
    It allows you to keep track of a number and increment it by clicking on a button.
    

But the one thing we can’t migrate is all the Vue things. After all, this is Markdown file and not a Vue file. So what do we do next?

Introducing Vue components in Markdown
--------------------------------------

If we want to add something with reactivity and utilize Vue, it’s time for us to talk about Vue components in Markdown.

To use Vue component in Markdown, the main thing we need to do is create a folder within the `/components` directory called `content`. In other words, these are components that we want to expose directly to the content that we are creating.

Once we do that, let’s go ahead and migrate all that remaining logic and code into a Counter.vue file.

📄 **/components/content/Counter.vue**

    <script setup>
    const currentCount = ref(0)
    
    const incrementCount = () => {
      currentCount.value++
    }
    </script>
    
    <template>
      <div class="counter">
        <p class="current-count">
          Current Count: <strong>{{ currentCount }}</strong>
        </p>
        <button @click="incrementCount">Add 1</button>
      </div>
    </template>
    
    <style>
    .counter {
      max-width: 500px;
      padding: 15px;
      margin: 0 auto;
      border: 3px solid #ccc;
      text-align: center;
    }
    
    .counter .current-count {
      margin-bottom: 10px;
      text-align: center;
      font-size: 1.5rem;
    }
    
    .counter button {
      font-size: 1rem;
      padding: 5px;
    }
    </style>
    

Now, to call our component within our Markdown file, we can call it directly just like you see here:

📄 **/content/blog/my-second-blog-post.md**

    ---
    title: What is a counter?
    ---
    
    ## What is a counter?
    
    It allows you to keep track of a number and increment it by clicking on a button.
    
    <Counter></Counter>
    

Now, in case you see that the page is no longer rendering, don’t worry! We’re going to take care of that in a future lesson where we instruct Nuxt how to render out our Markdown pages within the `pages` directory of our app.

Let’s ReVue
-----------

In this lesson, we learned about how Nuxt Content empowers us to go beyond the limitations of Markdown by allowing us to embed Vue components for a powerful workflow to create dynamic content!

To learn more about this, check out the [official docs on using Vue components with Nuxt Content v2](https://content.nuxtjs.org/v1/getting-started/writing/#vue-components).

### Lesson Resources

##### Source Code:

*   [Starting Code](https://github.com/Code-Pop/build-a-blog-with-nuxt-3-and-nuxt-content-v2/tree/04-begin)
    
*   [Ending Code](https://github.com/Code-Pop/build-a-blog-with-nuxt-3-and-nuxt-content-v2/tree/04-end)
