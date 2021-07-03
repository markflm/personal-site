<template>
  <div>
    <Scene :showAnimation="this.showAnimation" />
  </div>
  <div class="contentContainer">
    <div class="nav">
      <Navbar />
      <!-- TODO: take nav outside grid, stuff it in a flexbox with itself & the grid -->
    </div>
    <div class="contentGrid">
      <div class="aboutTitle" id="home">
        <div>Hi, I'm Mark</div>
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
:root {
  --dark-bg: rgba(24, 86, 122, 0.26);
  --dark-bg-opaque: rgb(10, 36, 51);
  --spacing: 200px;
  font-family: "League Spartan Bold", arial;
  font-size: 20px;
}

body::-webkit-scrollbar {
  width: 0.5rem;
}
body::-webkit-scrollbar-track {
  background: rgb(20, 20, 20);
}

body::-webkit-scrollbar-thumb {
  background: var(--dark-bg);
}
.contentContainer {
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  position: absolute;
}
.contentGrid {
  flex: 2;
  top: 0;
  left: 0;
  color: white;
  z-index: 99;
  position: absolute;
  width: 99%;
  overflow: hidden;
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  margin: 0px auto;
  padding-top: 120px;
  padding-bottom: 400px; /*extra padding for smooth scrolling to/from bottom anchor tag*/
}

.tester {
  grid-column: 10 / 11;
}
.aboutTitle {
  background: var(--dark-bg);
  grid-column: 3 / span 5;
  font-size: 2.5rem;
  padding: 2rem;
  margin-bottom: var(--spacing);
  display: flex;
  flex-direction: column;
  align-items: left;
}
/* .aboutTitle > .flexItem {
  border-top: 2px solid white;
} */
.nav {
  background: var(--dark-bg-opaque);
  height: 100vh;
  width: 8.5%;
  position: fixed;
  z-index: 100;
  transition: width 250ms ease;
}

.nav:hover {
  width: 14%;
}
.aboutMe {
  grid-column: 3 / 10;
}
.aboutHeader {
  font-size: 40pt;
}

.portfolio {
  grid-column: 3 / 10;
}
.contact {
  grid-column: 3/ 10;
}
.section {
  background: var(--dark-bg);
  font-size: 1.5rem;
  padding: 2rem;

  margin-bottom: var(--spacing);
}
</style>
