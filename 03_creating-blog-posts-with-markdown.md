Creating Blog Posts with Markdown
=================================

With a plugin like Nuxt Content, one of the things you might have noticed is that there isn’t any Markdown files to be found in the project! 🙀 And if this is your first time using Markdown, no worries, I got you covered in this lesson to provide a foundational overview. So let’s jump right in, shall we?

Where should Markdown content live?
-----------------------------------

Before we create our first piece of content though, we need to know where the Markdown files should live. And by default, Nuxt Content unsurprisingly sets the default folder to be called `content`. This means any content you want to have Nuxt watch (e.g., Markdown, YAML, CSV and JSON) should be placed in here. We’ll learn how to access these files later in the course.

If you’d like to learn more about how to configure this, you can check out [the official docs on configuring the source](https://content.nuxtjs.org/api/configuration#sources).

One of the advantages of using Nuxt Content is that it also respects folder hierarchy when it comes to organizing your files. In our case, this is helpful because in most sites, you don’t want all of your content sitting in a single directory. For example, you probably want your blog content to live in a `blog` directory. And then if you have a JSON file that contains all your social media handles, that might live in a different place of your own choosing.

So, to show that in action, let’s go ahead and create a new Markdown file in our `content/blog` directory.

    .
    ├── components
    ├── content
    │   └── blog
    │       └── my-first-blog-post.md
    └── pages
    

Next, we’ll go ahead and copy the contents of the `pages/blog/my-first-blog-post.vue` file into our Markdown file to show why Markdown makes content management that much easier.

Introducing Frontmatter
-----------------------

Before we talk about Markdown conversion though, an important feature about Markdown that you might not know about is frontmatter.

Frontmatter is an important standard that allows you to define custom metadata properties relevant to your content which really enriches the value of the content you’re providing to your audience. Examples include things like: tags, publish date, last updated date, etc.

It’s structured after [YAML](https://yaml.org/) syntax, which I won’t be covering here, but think of it as an alternative to JSON syntax that is a little cleaner to manage for this type of data.

Here’s an example of what it might look like:

    ---
    title: My First Blog Post
    episode: 482
    ---
    

In this example, we have defined two properties about the file:

1.  A `title` property with a value of `My First Blog Post`
2.  An `episode` property with a value of `482`

And while this might seem fairly simplistic at first, it makes a huge difference later on when you’re able to query files and render different files depending on its properties (like only fetching blog posts with certain tags).

Converting HTML to Markdown
---------------------------

When we copied our content over from `pages/blog/my-first-blog-post.vue` to `content/blog/my-first-blog-post.vue`, it probably looked something like this:

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
    
    <blockquote>
      <p>Blockquote</p>
    </blockquote>
    
    <p>
      And <strong>bold</strong>, <em>italics</em>.
    
      <a href="<https://markdowntohtml.com>">A link</a> to somewhere.
    </p>
    
    <p>And code highlighting:</p>
    
    <pre><code class="lang-js"><span class="hljs-keyword">var</span> foo = <span class="hljs-string">'bar'</span>;
    
    <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">baz</span><span class="hljs-params">(s)</span> </span>{
    <span class="hljs-keyword">return</span> foo + <span class="hljs-string">':'</span> + s;
    }
    </code></pre>
    
    <p>The end ...</p>
    

And while this might not seem intimidating at first, can you imagine what it would be like to make changes to this document? I don’t know about you, but the `pre` code block at the bottom definitely gives me the chills 😱.

Let’s go ahead and show how much simpler the content can be managed by migrating over to Markdown.

### Headings in Markdown

Let’s start by converting out all of our headings (i.e., h1, h2, etc.) to Markdown. The way we do this is to prefix our content with the X number of `#` symbols depending on what level the heading is.

*   `<h1>Heading 1</h1>` would become `# Heading 1`
*   `<h2>Heading 2</h2>` would become `## Heading 2`
*   `<h3>Heading 3</h3>` would become `### Heading 3`
*   And so on…

So, for our blog post, if we convert everything correctly, it should now look like:

    # Sample Markdown
    
    <p>This is some basic, sample markdown.</p>
    
    ## Second Heading
    
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
    
    <blockquote>
      <p>Blockquote</p>
    </blockquote>
    
    <p>
      And <strong>bold</strong>, <em>italics</em>.
    
      <a href="<https://markdowntohtml.com>">A link</a> to somewhere.
    </p>
    
    <p>And code highlighting:</p>
    
    <pre><code class="lang-js"><span class="hljs-keyword">var</span> foo = <span class="hljs-string">'bar'</span>;
    
    <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">baz</span><span class="hljs-params">(s)</span> </span>{
    <span class="hljs-keyword">return</span> foo + <span class="hljs-string">':'</span> + s;
    }
    </code></pre>
    
    <p>The end ...</p>
    

### Paragraphs and Inline Formatting in Markdown

Since paragraphs are the most common element when writing any content, they are the easiest element to create / manage since they don’t have any signifiers!

*   `<p>My text</p>` would become `My text`

In other words, any new line of text in Markdown is assumed to be a paragraph!

And when you want to add bold or italic, those are respectfully defined using:

*   `*Bold Text**` for `<strong>Bold Text</strong>`
*   `_Italic Text_` for `<em>Italic Text</em>`

Applying this to our blog post, it should now look like:

    # Sample Markdown
    
    This is some basic, sample markdown.
    
    ## Second Heading
    
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
    
    <blockquote>
      <p>Blockquote</p>
    </blockquote>
    
    And **bold**, _italics_.
    
    <a href="<https://markdowntohtml.com>">A link</a> to somewhere.
    
    And code highlighting:
    
    <pre><code class="lang-js"><span class="hljs-keyword">var</span> foo = <span class="hljs-string">'bar'</span>;
    
    <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">baz</span><span class="hljs-params">(s)</span> </span>{
    <span class="hljs-keyword">return</span> foo + <span class="hljs-string">':'</span> + s;
    }
    </code></pre>
    
    The end ...
    

### Links and Blockquotes

Links in Markdown consist of two signifiers: square brackets `[]` and parentheses `()` immediately following it.

The content within the square brackets defines what the link text will be, while the parentheses defines what URL the link should go to.

*   `[Vue Mastery](<https://www.vuemastery.com>)` is equivalent to `<a href="<https://www.vuemastery.com>">Vue Mastery</a>`

Blockquotes in Markdown are prefixed with the grater than symbol (i.e., `>`).

*   `> My Quote` is equivalent to `<blockquote><p>My Quote</p></blockquote>`

Applying these to our blog post, we get

    # Sample Markdown
    
    This is some basic, sample markdown.
    
    ## Second Heading
    
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
    
    > Blockquote
    
    And **bold**, _italics_.
    
    [A link](<https://markdowntohtml.com>) to somewhere.
    
    And code highlighting:
    
    <pre><code class="lang-js"><span class="hljs-keyword">var</span> foo = <span class="hljs-string">'bar'</span>;
    
    <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">baz</span><span class="hljs-params">(s)</span> </span>{
    <span class="hljs-keyword">return</span> foo + <span class="hljs-string">':'</span> + s;
    }
    </code></pre>
    
    The end ...
    

### Lists in Markdown

Lists are a common thing people use in content, and luckily managing lists uses syntax that you probably use naturally when having to jot down lists of your own:

*   Unordered list items are prefixed with a dash \`\`
*   Ordered list items are prefixed with the system you want to use. For example, a numbered list would use the number as a prefix (e.g., `1.` )

So, for our list in our blog post, it would be converted to:

    # Sample Markdown
    
    This is some basic, sample markdown.
    
    ## Second Heading
    
    - Unordered lists, and:
      1. One
      2. Two
      3. Three
    - More
    
    > Blockquote
    
    And **bold**, _italics_.
    
    [A link](<https://markdowntohtml.com>) to somewhere.
    
    And code highlighting:
    
    <pre><code class="lang-js"><span class="hljs-keyword">var</span> foo = <span class="hljs-string">'bar'</span>;
    
    <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">baz</span><span class="hljs-params">(s)</span> </span>{
    <span class="hljs-keyword">return</span> foo + <span class="hljs-string">':'</span> + s;
    }
    </code></pre>
    
    The end ...
    

### Code Blocks

Finally, code blocks in Markdown might be one of the greatest time savers for writing content, because all you need is the triple back ticks and what language it is defined on the first line

    ```js
    const message = "Isn't this cool?"
    

    
    In this example, we've defined a code block that contains JavaScript for syntax highlighting to work as intended later on.
    
    So when we apply this to our blog post, we get:
    
    ```markdown
    # Sample Markdown
    
    This is some basic, sample markdown.
    
    ## Second Heading
    
    - Unordered lists, and:
      1. One
      2. Two
      3. Three
    - More
    
    > Blockquote
    
    And **bold**, _italics_.
    
    [A link](<https://markdowntohtml.com>) to somewhere.
    
    And code highlighting:
    
    ```js
    var foo = 'bar';
    
    function baz(s) {
      return foo + ':' + s;
    }
    

The end …

    
    Doesn't that look way better? Modifying that code block now can now be as easy as copying and pasting snippets directly from your code editor rather than having to do all that conversion so it renders and highlights as intended.
    
    ## Let's ReVue
    
    Now, doesn't our blog post look way simpler than what we had before in the Vue file? Can you imagine creating a Vue file for every single blog post that you had? 😵‍💫
    
    In this lesson, we've covered:
    
    - how Markdown is stored and managed by Nuxt Content in the `content` directory
    - what frontmatter is and why it's a powerful standard to use for Markdown files
    - fundamental Markdown syntax to get people started creating and managing content
    
    And the incredible part is that this is just the beginning of what's possible for Markdown in helping users manage and create content in a more maintainable way.

    ### Lesson Resources

##### Source Code:

*   [Starting Code](https://github.com/Code-Pop/build-a-blog-with-nuxt-3-and-nuxt-content-v2/tree/03-begin)
    
*   [Ending Code](https://github.com/Code-Pop/build-a-blog-with-nuxt-3-and-nuxt-content-v2/tree/03-end)
