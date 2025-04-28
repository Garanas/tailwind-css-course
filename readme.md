# Tailwind Course

This repository is my personal interpretation of a [course](https://www.youtube.com/watch?v=lCxcTsOHrjo) about the use of [Tailwind](https://tailwindcss.com/) by [Dave Gray](https://yesdavidgray.com/). I deviate from the course by using [Astro](https://astro.build/).

## Encountered issues

While going through the course I encountered some issues. They are described here. These are not necessarily issues with the (content of) the course. They are likely issues because of my lack of understanding (of Astro).

### Defining content

The use of `before:content-['\201C']` appears to break the build pipeline of Astro. The moment I use this the component is no longer rendered properly - parts of the HTML of the component appear to be missing in the output. 

The HTML in the component:

```html
<figure class="my-12">
    <blockquote class="bg-teal-600 dark:bg-black pl-14 pr-8 py-12 rounded-3xl relative">
        <p class="text-2xl sm:text-3xl text-left mt-2 text-white dark:text-slate-400 before:content-['\201C'] before:font-serif before:absolute before:top-0 before:left-0 before:text-9xl before:text-white before:opacity-25 before:transform before:translate-x-2 before:translate-y-2 after:content-['\201D'] after:font-serif after:absolute after:-bottom-20 after:right-0 after:text-9xl after:text-white after:opacity-25 after:transform after:-translate-x-2 after:-translate-y-2">
            <slot>
        </p>
    </blockquote>
    <figcaption class="italic text-xl sm:text-2xl text-right mt-2 text-slate-500 dark:text-slate-400">
        - Wile E. Coyote, Genius
    </figcaption>
</figure>
```

The output of the component on the page:

```html
Acme
has always been there
for me. Their Explorer rocket arrived in a wooden crate as expected.
Life-long customer! A++ shopping experience.
<p></p>
<figcaption class="italic text-xl sm:text-2xl text-right mt-2 text-slate-500 dark:text-slate-400">
    - Wile E. Coyote, Genius
</figcaption>
```

I got around this by using spans to represent the quotes. The output matches the input and is as you'd expect:

```html
<figure class="my-12">
    <blockquote class="bg-teal-600 dark:bg-black pl-14 pr-8 py-12 rounded-3xl relative">
       <span class="absolute top-0 left-4 text-9xl text-white opacity-25 font-serif transform translate-x-2 translate-y-2">“</span> 
       <p class="text-2xl sm:text-3xl text-left mt-2 text-white dark:text-slate-400"> 
          Acme
          has always been there
          for me. Their Explorer rocket arrived in a wooden crate as expected.
          Life-long customer! A++ shopping experience.
       </p>
       <span class="absolute bottom-0 right-4 text-9xl text-white opacity-25 font-serif transform -translate-x-2 translate-y-16">”</span> 
    </blockquote>
    <figcaption class="italic text-xl sm:text-2xl text-right mt-2 text-slate-500 dark:text-slate-400">
       - Wile E. Coyote, Genius 
    </figcaption>
</figure>
```

### Tailwind configuration

In the most recent version of tailwind the configuration is not available by default. The Tailwind team introduced a [css-first configuration](https://tailwindcss.com/blog/tailwindcss-v4#css-first-configuration). You can still [introduce the standard configuration file](https://github.com/tailwindlabs/tailwindcss/discussions/17168#discussioncomment-12734594). A lot of novice users that use tutorials using v3 or earlier are caught off guard by this, up to the point that there's [YouTube videos](https://www.youtube.com/watch?v=bupetqS1SMU) by other authors to inform people about it!

## Feedback on the course

These are some things that I would like to see different in this course. This section is by all means my opinion and as with any other opinion - it's fine to disagree. Just don't be an asshole about it.

### Type after me

The course is about learning Tailwind. There's a separate [course](https://www.youtube.com/playlist?list=PL0Zuz27SZ-6Mx9fd9elt80G1bPcySmWit) by the same author to learn about Cascading Style Sheets (CSS). The course about CSS is referenced multiple times in this course about Tailwind. Therefore I feel it is safe to assume that the author expects the audience to have an understanding of CSS before they start with this course about Tailwind.

In practice you often implement a website design. You can analyze the design from top to bottom. And as you do that, you identify chunks of the website like a header or a hero section. You can then analyze these chunks separately by figuring out the HTML hierarchy and what CSS properties you need on each HTML tag to recreate that chunk. Once you have a good understanding of the design you can proceed to build it.

One selling point is the ability to build an interface by applying small, atomic [utility classes](https://tailwindcss.com/docs/styling-with-utility-classes) in your HTML markup. You can see the output update live as you apply classes. This removes the need to think about the name of the class. It removes the need to work in different files. You can focus on what you discovered during your analysis and apply them one by one: You apply flex, add children and center the items. Save and review. You introduce padding a gap. Save and review. You can continue this until it matches the intended design. By using Tailwind, it becomes a fast and iterative process with a focus on the result.

This is where my feedback starts. The course does have an example of what we want to build. We could consider this example to be the design. A minor caveat: the author does not use GitHub Pages to allow the audience to look at the end result at their own pace. The author does show the end result a few times while instructing the viewer on what to type. The author makes use of [Emmet abbreviations](https://docs.emmet.io/abbreviations/). This is great if you have a good understanding of HTML, CSS and Tailwind. But we're talking about an tutorial here that introduces the viewer to Tailwind. We can not expect the audience to have a good understanding of these concepts, at least not early on in the course. By using Emmet abbreviations both the author and the viewer essentially skip the iterative process all together. Which is something you can expect from an expert because he built a similar interface a thousand times before. But you can not expect this from a pre-novice - the audience of this course.

To conclude, the use of Emmet abbreviations makes it more difficult to work iteratively. And the analysis - why are these classes applied - is in my opinion skipped. I did not understand what the author was trying to built at every stage. All I could do was type along and hope that I would not make a typo. Just to immediately jump to the next component and repeat the typing. It would've been better in my opinion if the author would first dissect the website. Bring up the docs of Tailwind to see what we need while dissecting the design. And then gradually apply the classes, while reviewing the intermediate result to make sure our analysis is in the right direction.

### Do not repeat yourself

The Do Not Repeat, or DRY for short, principle is still [a hot topic to this day](https://thevaluable.dev/dry-principle-cost-benefit-example/). It should definitely not always be applied as if it is a holy grail. I understand that the author of the course wants to focus on just Tailwind, without the use of a framework. It allows the viewer to see and understand Tailwind on its own and I can appreciate that.

This is where my feedback starts. I must admit that the moment the author stated working on the testimonials section I had a shiver. The shiver turned into a slight terror when the author started working on the first quote. This specifically happened as the author was writing the [paragraph with 28 different classes applied to it](https://github.com/gitdagray/tailwind-css-course/blob/main/lesson03/build/index.html#L940). The only thing I was thinking of: for the love of god, please tell me there's only one quote on this page. There were three.

It is a great candidate to not repeat. It could be part of a component. But that is not possible because of the lack of a framework. And therefore I feel the author should have opted for a different solution that provides the same result.

To make it more concrete, this is the relevant code:

```lua
<figure class="my-12">
    <blockquote class="bg-teal-600 dark:bg-black pl-14 pr-8 py-12 rounded-3xl relative">
        <p
            class="text-2xl sm:text-3xl text-left mt-2 text-white dark:text-slate-400 before:content-['\201C'] before:font-serif before:absolute before:top-0 before:left-0 before:text-9xl before:text-white before:opacity-25 before:transform before:translate-x-2 before:translate-y-2 after:content-['\201D'] after:font-serif after:absolute after:-bottom-20 after:right-0 after:text-9xl after:text-white after:opacity-25 after:transform after:-translate-x-2 after:-translate-y-2">
            Acme
            has always been there
            for me. Their Explorer rocket arrived in a wooden crate as expected.
            Life-long customer! A++ shopping experience.
        </p>
    </blockquote>
    <figcaption class="italic text-xl sm:text-2xl text-right mt-2 text-slate-500 dark:text-slate-400">
        &#8212;Wile E. Coyote, Genius
    </figcaption>
</figure>
```

One solution would be to encapsulated the classes in a custom class using the [@apply](https://tailwindcss.com/docs/functions-and-directives#apply-directive) directive. The author used this directive in lesson 4 to encapsulate classes for the animated menu. Another solution would be to adjust the structure of the HTML:

```html
<figure class="my-12">
    <blockquote class="bg-teal-600 dark:bg-black pl-14 pr-8 py-12 rounded-3xl relative">
       <span class="absolute top-0 left-4 text-9xl text-white opacity-25 font-serif transform translate-x-2 translate-y-2">“</span> 
       <p class="text-2xl sm:text-3xl text-left mt-2 text-white dark:text-slate-400"> 
          Acme
          has always been there
          for me. Their Explorer rocket arrived in a wooden crate as expected.
          Life-long customer! A++ shopping experience.
       </p>
       <span class="absolute bottom-0 right-4 text-9xl text-white opacity-25 font-serif transform -translate-x-2 translate-y-16">”</span> 
    </blockquote>
    <figcaption class="italic text-xl sm:text-2xl text-right mt-2 text-slate-500 dark:text-slate-400">
       - Wile E. Coyote, Genius 
    </figcaption>
</figure>
```

It's visually the same. But it's much easier to reason about. I'm not sure whether it behaves different when accessibility is a concern. To conclude, I feel like this was a missed opportunity to highlight how the audience can work with Tailwind when Tailwind becomes a little verbose. And how there are different solutions to overcome this.

## Resources used in the course

- [Tailwind CSS Course by Dave Gray](https://www.youtube.com/watch?v=lCxcTsOHrjo)
- [Emoji library ](https://emojipedia.org)
- [Symbol Codes (Symbl.cc)](https://symbl.cc/)
