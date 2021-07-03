<template>
  <ul class="navInternal">
    <!-- TODO: change to font-awesome svgs -->
    <li @click="scrollToSection('home')">Home</li>
    <li @click="scrollToSection('about')">About</li>
    <li @click="scrollToSection('portfolio')">Portfolio</li>
    <li @click="scrollToSection('cin')">Contact</li>
  </ul>
</template>

<script>
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
.navInternal {
  padding: 0;
  list-style: none;
  display: flex;
  flex-direction: column;
  margin-top: 200px;
  margin-bottom: 20px;
  margin-right: 20px;
  margin-left: 5px;
  justify-content: space-between;
  align-content: space-between;
  align-items: center;
  justify-items: flex-start;
  height: 50%;
  color: white;
}

.navInternal > li {
  border-bottom: 1px solid white;
  width: 100%;
  display: flex;
  align-items: center;
  cursor: pointer;
}
</style>