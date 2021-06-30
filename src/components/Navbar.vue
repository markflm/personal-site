<template>
  <div class="navInternal">
    <div @click="scrollToSection('home')">Home</div>
    <div @click="scrollToSection('about')">About</div>
    <div @click="scrollToSection('portfolio')">Portfolio</div>
    <div @click="scrollToSection('cin')">Contact</div>
  </div>
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

.navInternal > div {
  border-bottom: 1px solid white;
  width: 100%;
  text-align: center;
  cursor: pointer;
}
</style>