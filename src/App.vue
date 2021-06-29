<template>
  <div>
    <Scene :showAnimation="this.showAnimation" />
  </div>
  <div class="contentGrid">
    <div class="aboutTitle">
      <div>Mark Craven</div>
      <div class="flexItem">Full Stack Developer</div>
    </div>
    <div class="section aboutMe">
      <div class="aboutHeader">I go on the computer</div>
      that's right I do
    </div>
  </div>
</template>

<script>
import Scene from "./components/Scene.vue";

export default {
  name: "App",
  components: {
    Scene,
  },
  data() {
    return {
      showAnimation: true,
    };
  },
};
</script>

<style>
:root {
  --dark-bg: rgba(24, 86, 122, 0.26);
  --spacing: 200px;

  font-family: brandon-grotesque, sans-serif;
  font-weight: 400;
  font-style: normal;
}
.contentGrid {
  color: white;
  z-index: 99;
  position: absolute;
  width: 99%;
  overflow: hidden;
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  margin: 0px auto;
  padding: 120px 0px;
}

.aboutTitle {
  background: var(--dark-bg);
  grid-column: 4 / span 5;
  font-size: 2.5rem;
  padding: 2rem;
  margin-bottom: var(--spacing);
  display: flex;
  flex-direction: column;
  align-items: center;
}
.aboutTitle > .flexItem {
  border-top: 2px solid white;
}
.aboutMe {
  grid-column: 2 / 10;
}
.aboutHeader {
  font-size: 40pt;
}

.section {
  background: var(--dark-bg);
  font-size: 1.5rem;
  padding: 2rem;
  margin-bottom: var(--spacing);
}
</style>
