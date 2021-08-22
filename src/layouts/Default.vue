<template>
  <div class="layout" :class="{ 'sticky-header': this.$route.path === '/' }">
    <header class="header" :class="{ sticky: this.$route.path === '/' }">
      <div class="container">
        <div class="left">
          <g-link to="/" class="home-link">
            <img src="/logo.svg" alt="Alan Ciao" class="logo">
          </g-link>
        </div>
        <nav class="nav right">
          <g-link to="/journal" class="nav__link">Journal</g-link>
          <g-link to="/contact" class="nav__link">Say Hi!</g-link>
        </nav>
      </div>
    </header>

    <slot/>

    <footer class="footer">
      <div class="container">
        <span>Copyright © 2021</span>
      </div>
    </footer>
  </div>
</template>

<style scoped>
.header {
  position: relative;
  height: 6rem;
  z-index: 10;
}
.header.sticky {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
}
.header > .container {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 100%;
}
.home-link {
  text-decoration: none;
}
.logo {
  height: 1.5rem;
}

.nav > * {
  font-size: .9rem;
  font-weight: 600;
  text-decoration: none;
  margin-top: 4px;
  margin-right: 3rem;
  padding-bottom: 4px;
  border-bottom: 1px solid;
  border-color: transparent;
  transition: border .15s;
}
.nav > *:last-of-type {
  margin: 0;
}
.nav > .active, .nav > *:hover {
  border-color: inherit;
}

.footer {
  font-size: .8rem;
  padding: 6rem 0;
}
</style>
