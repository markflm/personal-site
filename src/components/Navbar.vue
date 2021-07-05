<template>
  <ul class="navInternal">
    <!-- TODO: change to font-awesome svgs -->
    <div class="navContent">
      <li @click="scrollToSection('home')">Home</li>
      <li @click="scrollToSection('about')">About</li>
      <li @click="scrollToSection('portfolio')">Portfolio</li>
      <li @click="scrollToSection('cin')">Contact</li>
    </div>
  </ul>
</template>

<script>
//TODO: add wrapper over list items that only covers ~50% of nav. can justify-content in there to give items desired spacing
export default {
  name: "Navbar",
  methods: {
    scrollToSection(id) {
      const element = document.getElementById(id);
      console.log(element);
      element.scrollIntoView({ top: 0, behavior: "smooth" });
    },
  },
};
</script>

<style>
@import "../css/styles.css";

.navInternal {
  padding: 0;
  margin: 0;
  list-style: none;
  width: 10.5%;
  background: var(--dark-bg-opaque);
  height: 100vh;
  position: fixed;
  z-index: 100;
  color: white;
  transition: width 225ms ease;
}

.navContent {
  height: 50%;
  width: 50%;
  list-style: none;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-content: space-between;
  padding-top: 50px;
}
.navInternal:hover {
  width: 14%;
}
.navInternal > .navContent > li {
  list-style: none;
  border-bottom: 1px solid white;
  display: flex;
  align-self: flex-start;
  cursor: pointer;
}
</style>