<template>
  <header class="header" :class="{ hidden: !showNavbar && !mobileNavActive }">
    <nav v-if="navLinks" class="navigation left desktop-nav">
      <ul>
        <router-link
          v-for="nav in navLinks"
          :key="nav.text"
          v-if="nav.position === 'left' && !nav.external"
          tag="li"
          :to="nav.link"
          active-class="active"
          v-text="nav.text"
          exact
        />
        <li
          v-for="nav in navLinks"
          v-if="nav.position === 'left' && nav.external"
        >
          <a :href="nav.link" target="_blank">{{ nav.text }}</a>
        </li>
      </ul>
    </nav>

    <div class="brand">
      <router-link to="/">
        <div
          v-if="logo"
          class="logo"
          :style="{ backgroundImage: `url(${logo})` }"
          :title="$site.title"
        />
        <span v-else>{{ $site.title }}</span>
      </router-link>
    </div>

    <nav v-if="navLinks" class="navigation right desktop-nav">
      <ul>
        <router-link
          v-for="nav in navLinks"
          :key="nav.text"
          v-if="nav.position === 'right' && !nav.external"
          tag="li"
          :to="nav.link"
          active-class="active"
          v-text="nav.text"
          exact
        />
        <li
          v-for="nav in navLinks"
          v-if="nav.position === 'right' && nav.external"
        >
          <a :href="nav.link" target="_blank">{{ nav.text }}</a>
        </li>
      </ul>
    </nav>
    <Hamburger class="mobile-nav-toggle" @toggle="toggleMobileNav" />
    <div class="mobile-nav" :class="{ 'mobile-nav--active': mobileNavActive }">
      <nav>
        <ul @click="toggleMobileNav">
          <router-link
            v-for="nav in navLinks"
            :key="nav.text"
            v-if="!nav.external"
            tag="li"
            :to="nav.link"
            active-class="active"
            v-text="nav.text"
            exact
          />
          <li
            v-for="nav in navLinks"
            v-if="nav.external"
            @click="toggleMobileNav"
          >
            <a :href="nav.link" target="_blank">{{ nav.text }}</a>
          </li>
        </ul>
        <div class="mobile-nav-close" @click="toggleMobileNav" />
      </nav>
    </div>
  </header>
</template>

<script>
export default {
  created() {
    if (typeof window !== "undefined") {
      window.addEventListener("scroll", this.handleScroll);
    }
  },
  destroyed() {
    if (typeof window !== "undefined") {
      window.removeEventListener("scroll", this.handleScroll);
    }
  },
  props: {
    logo: {
      type: String,
      required: false,
    },
  },
  data() {
    return {
      mobileNavActive: false,
      showNavbar: true,
      lastScrollPosition: 0,
    };
  },
  computed: {
    navLinks() {
      return this.$site.themeConfig.nav;
    },
  },
  methods: {
    toggleMobileNav(hamburgerOpen) {
      this.mobileNavActive = hamburgerOpen;
    },
    handleScroll(event) {
      if (typeof window !== "undefined") {
        if (window.pageYOffset < 0) {
          return;
        }
        if (Math.abs(window.pageYOffset - this.lastScrollPosition) < 60) {
          return;
        }
        this.showNavbar = window.pageYOffset < this.lastScrollPosition;
        this.lastScrollPosition = window.pageYOffset;
      }
    },
  },
};
</script>

<style scoped>
.header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: var(--space-3xl);
  padding-left: var(--space-screen-border);
  padding-right: var(--space-screen-border);
  font-size: var(--space-m);
  font-weight: 600;
  z-index: 10;
  position: fixed;
  width: 100%;
  transform: translate3d(0, 0, 0);
  transition: 0.3s all ease-out;
  top: 0;
}

.header.hidden {
  box-shadow: none;
  transform: translate3d(0, -100%, 0);
}

.logo {
  position: absolute;
  width: var(--space-xxl);
  height: max(50px, 8vw);
  background-size: contain;
  background-position: center;
  background-repeat: no-repeat;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
}

.navigation li {
  display: inline-block;
  list-style: none;
  margin-right: 1rem;
  user-select: none;
  cursor: pointer;
  border-bottom: 1px solid transparent;
}

.navigation li:last-of-type {
  margin: 0;
}

.navigation li:hover {
  border-bottom: 1px solid var(--color-black);
}

.active {
  border-bottom: 1px solid var(--color-black);
}

a {
  text-decoration: none;
  color: inherit;
}

a:active {
  color: inherit;
}
a:visited {
  color: inherit;
}

.desktop-nav {
  display: none;
}

.mobile-nav {
  display: block;
  position: absolute;
  background: #ffffff;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  padding: 2rem;
  transform: translateY(-100%);
  transition: transform 0.5s ease-in-out;
  text-align: center;
  font-size: 2rem;
  display: flex;
  justify-content: center;
  align-items: center;
  line-height: 2;
}

.mobile-nav li {
  list-style: none;
  cursor: pointer;
  transition: opacity 0.15s;
}

.mobile-nav li:hover {
  opacity: 0.6;
}

.mobile-nav--active {
  transform: translateY(0);
}

.mobile-nav-toggle {
  display: block;
  width: var(--space-xl);
  height: var(--space-xl);
  transition: opacity 0.15s;
  cursor: pointer;
  fill: none;
  stroke: var(--color-black);
  stroke-miterlimit: 10;
  stroke-width: 10;
  stroke-linecap: round;
  z-index: 11;
}

@media screen and (min-width: 600px) {
  .header {
    box-shadow: 0px 0px 10px rgb(212, 211, 211);
    background-color: rgba(255, 255, 255, 0.9);
  }
  .desktop-nav {
    display: block;
  }
  .mobile-nav-toggle {
    display: none;
  }
  .mobile-nav {
    display: none;
  }
}
</style>
