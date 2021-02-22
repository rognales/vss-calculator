<template>
  <div>
    <nav
      class="navbar header has-shadow is-dark"
      role="navigation"
      aria-label="main navigation"
    >
      <div class="navbar-brand">
        <a class="navbar-item" href="/"> Calculator </a>

        <div class="navbar-burger">
          <span />
          <span />
          <span />
        </div>
      </div>
    </nav>

    <section class="main-content columns">
      <div class="container column is-12">
        <nuxt />
      </div>
    </section>
    <footer class="footer">
      <div class="content has-text-centered">
        <p>
          <strong>VSS Calculator</strong> by
          <span class="has-text-primary">@rognales</span>
        </p>
      </div>
      <div class="columns is-centered p-4">
        <div class="column is-half">
          <nav class="level is-mobile">
            <p class="level-item has-text-centered">
              <img src="~/assets/nuxtjs.svg" alt="" style="height: 30px" />
            </p>
            <p class="level-item has-text-centered">
              <img src="~/assets/buefy.png" alt="" style="height: 30px" />
            </p>
          </nav>
        </div>
      </div>
    </footer>
  </div>
</template>

<script>
export default {
  data() {
    return {
      items: [
        {
          title: "Home",
          icon: "home",
          to: { name: "index" },
        },
        {
          title: "Inspire",
          icon: "lightbulb",
          to: { name: "inspire" },
        },
      ],
    };
  },
};
</script>
