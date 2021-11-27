<template>
  <div class="wrapper">
    <Navbar :logo="$site.themeConfig.logo" :sticky="$route.path === '/'" />

    <div class="container">
      <!-- Works list -->
      <div v-if="$route.path === '/'">
        <Content />
      </div>

      <!-- Single project view -->
      <div v-if="isSingleProject">
        <SingleProjectHeader
          :title="$page.frontmatter.title"
          :year="$page.frontmatter.year.toString()"
          :categories="$page.frontmatter.categories"
        />
        <Content />
      </div>

      <!-- Journal list -->
      <div v-if="$route.path === '/journal/'" class="journal-list">
        <Content />
      </div>

      <!-- Single journal -->
      <div v-if="isSingleJournal" class="single-journal">
        <Content />
      </div>
    </div>

    <!--<Footer />-->
  </div>
</template>

<script>
export default {
  computed: {
    isSingleProject() {
      const worksRoute = "/works/";
      const path = this.$route.path;
      if (path.includes("works") && path.length >= worksRoute.length + 1) {
        return true;
      }
    },
    isSingleJournal() {
      const journalRoute = "/journal/";
      const path = this.$route.path;
      if (path.includes("journal") && path.length >= journalRoute.length + 1) {
        return true;
      }
    },
  },
  updated() {
    // unwrap all images from paragraph tags so we can have
    // different widths inside the content.

    document.querySelectorAll("p img").forEach((image) => {
      var wrapper = image.parentNode;
      let children = wrapper.children;
      let fragment = document.createDocumentFragment();

      Array.from(children).forEach((child) => {
        fragment.appendChild(child);
      });

      wrapper.parentNode.replaceChild(fragment, wrapper);
    });
  },
};
</script>

<style>
:root {
  --color-black: #1c1c1c;
  --color-highlight: rgba(249, 233, 172, 0.99);
  --space-unit: 1em;
  --space-xxs: calc(0.25 * var(--space-unit));
  --space-xs: calc(0.5 * var(--space-unit));
  --space-s: calc(0.75 * var(--space-unit));
  --space-m: calc(1.25 * var(--space-unit));
  --space-l: calc(2 * var(--space-unit));
  --space-xl: calc(3 * var(--space-unit));
  --space-xxl: calc(5 * var(--space-unit));
  --space-3xl: calc(7 * var(--space-unit));
  --space-4xl: calc(9 * var(--space-unit));
  --space-5xl: calc(11 * var(--space-unit));
  --space-screen-border: 5vw;
}

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

*::-moz-selection {
  background: var(--color-highlight);
  color: var(--color-black);
}

*::-webkit-selection {
  background: var(--color-highlight);
  color: var(--color-black);
}

*::selection {
  background: var(--color-highlight);
  color: var(--color-black);
}

body {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", "Roboto",
    "Noto Sans", "Ubuntu", "Droid Sans", "Helvetica Neue", sans-serif;
  font-size: 16px;
  background: #fff;
  color: var(--color-black);
}

img {
  width: 100%;
  max-width: 100%;
  line-height: 0;
  margin: 2rem 0;
}

.container {
  padding: var(--space-4xl) var(--space-screen-border);
  padding-bottom: var(--space-screen-border);
}

.journal-list,
.single-journal {
  width: 800px;
  max-width: 100%;
  margin: 0 auto;
}

h1,
h2,
h3,
h4,
h5,
h6,
p {
  width: 100%;
  max-width: 800px;
}

h1 {
  font-size: var(--space-xl);
  line-height: 1.15;
  font-weight: 300;
  margin: var(--space-xl) auto var(--space-xl) auto;
}

h2 {
  font-size: 2rem;
  font-weight: 300;
  margin: 2rem auto 2rem auto;
}

h3 {
  font-size: 1rem;
  font-weight: 700;
  margin: 2rem auto 1rem auto;
}

p {
  font-size: 1rem;
  line-height: 1.5;
  margin: 1rem auto 2rem auto;
}

pre {
  background: var(--color-black);
  padding: 1rem;
  margin: 1rem 0;
}

code {
  color: white;
  background: var(--color-black);
  font-size: 0.8rem;
  padding: 0.05rem 0.25rem;
  font-weight: 400;
}

@media screen and (max-width: 600px) {
  .container {
    padding-top: var(--space-xxl);
  }
}
</style>
