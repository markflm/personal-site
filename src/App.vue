<template>
  <div>
    <Scene :showAnimation="this.showAnimation" />
  </div>
  <div class="contentContainer">
    <Navbar />
    <!-- <div class="nav">
 <Navbar /> -->
    <!-- TODO: take nav outside grid, stuff it in a flexbox with itself & the grid -->
    <!-- </div> -->
    <div class="contentGrid">
      <div class="aboutTitle" id="home">
        <div>Hi, I'm Mark.</div>
        <div class="flexItem">Full Stack Web Developer</div>
      </div>
      <div class="section aboutMe" id="about">
        <div class="aboutHeader">I go on the computer</div>
        that's right I do
      </div>
      <div class="section portfolio" id="portfolio">Portfolio goes here</div>
      <div class="section contact" id="contact">
        <ContactForm />
      </div>
    </div>
  </div>
</template>

<script>
import Scene from "./components/Scene";
import Navbar from "./components/Navbar";
import ContactForm from "./components/ContactForm.vue";

export default {
  name: "App",
  components: {
    Scene,
    Navbar,
    ContactForm,
  },
  data() {
    return {
      showAnimation: true,
    };
  },
};
</script>

<style>
@import url(https://allfont.net/allfont.css?fonts=league-spartan);
@import "./css/styles.css";
</style>
