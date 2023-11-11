Introduction
============

A common thing that most developers need when it comes to their building their portfolio or whatnot is some sort of blog site. That’s always been kind of tricky to do, especially when you have third party dependencies. And frankly, writing content is hard enough without adding the complication of configuring tooling and all.

With the recent release of Nuxt Content v2 though, we thought it would be great to build a series where we show you how to build a blog using the [Nuxt 3](https://v3.nuxtjs.org/), [Nuxt Content v2](https://content.nuxtjs.org/) and [Bulma CSS](https://bulma.io/), just to provide some basic styles and layering on top.

Overview of the Tech Stack
--------------------------

Here’s a high level overview of the technology we’re using in this course.

*   [Nuxt 3](https://v3.nuxtjs.org/) is one of the most popular meta frameworks for the Vue ecosystem. It provides a ton of incredible developer experience enhancements and is worth taking a look at if you’ve never heard of it. We have an [introductory course](https://www.vuemastery.com/courses/nuxt-3-essentials/nuxt-3-overview) if you’d like to learn the fundamentals.
*   [Nuxt Content v2](https://content.nuxtjs.org/) is a plugin built to make it easy for you to manage from your local repository, rather than having to depend on a third party library. which is incredibly exciting. And there’s a whole slew of other things as well.
*   [Bulma CSS](https://bulma.io/) is an open source CSS library that provides a design system for developers to style components. After all, having content is great, but without good design it can make it the reading experience… less than desirable. 😅

Deeper Dive on Nuxt Content
---------------------------

When you take a look at the [blog post announcement for Nuxt Content v2](https://content.nuxtjs.org/blog/announcing-v2/), you will see that there is a bunch of new features.

![Nuxt Content V2](https://firebasestorage.googleapis.com/v0/b/vue-mastery.appspot.com/o/flamelink%2Fmedia%2FBuild%20a%20Blog%20with%20Nuxt%20Content%20v2%20(Lesson)%20-%2001-01%20-%20Blog%20Post.jpg?alt=media&token=448f8070-edd4-4bb1-970a-36b7e7bdf024)

At its core however, Nuxt Content allows us to easily work with local files for ingesting data. And since this a course about building a blog, you might be thinking imagining that it’s limited to Markdown files, but it’s way more than that. In addition to Markdown, you can also ingest YAML, CSV, and JSON files and pull them into your app!

One of the reasons this is great is because you get version control, guaranteed availability (i.e., no server outages to worry about), and much more, which is phenomenal for developers. And then on top of that, it comes with a lot of built-in developer experience enhancements, such as being able to easily render your markdown inside of your documents. And believe it or not, you can even use Vue components within your Markdown files as well! 🤯

This is exciting because now in addition to having standard text content, you now have the ability to get creative with how you want your content to be displayed while still leveraging the simplicity of markdown when it comes to managing your content. More on this in an upcoming lesson!

Let’s ReVue
-----------

In this lesson, we have covered a high level overview of the tech stack that we’ll be using for this course: [Nuxt 3](https://v3.nuxtjs.org/), [Nuxt Content v2](https://content.nuxtjs.org/) and [Bulma CSS](https://bulma.io/). In addition, we’ve taken a look at some of the great features that Nuxt Content offers us as developers in being able to manage content.

So with that said, let’s go ahead and take a look at an overview of the project!

### Lesson Resource

##### Source Code:

*   [Nuxt 3 Essentials](https://www.vuemastery.com/courses/nuxt-3-essentials/nuxt-3-overview/)
