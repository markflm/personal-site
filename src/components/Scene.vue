<template>
  <div id="three-scene"></div>
</template>

<script>
import * as THREE from "three";
import { OrbitControls } from "three/examples/jsm/controls/OrbitControls";
export default {
  name: "Scene",
  data() {
    return {};
  },
  mounted() {
    window.addEventListener("scroll", this.moveCamera);
    this.init();
    Array(200).fill().forEach(this.addStar);
    this.addProfilePic();
  },
  unmounted() {
    window.removeEventListener("scroll", this.moveCamera);
  },
  methods: {
    init() {
      this.scene = new THREE.Scene();
      this.camera = new THREE.PerspectiveCamera(
        75,
        window.innerWidth / window.innerHeight,
        0.1,
        1000
      );

      this.renderer = new THREE.WebGLRenderer();
      document
        .getElementById("three-scene")
        .appendChild(this.renderer.domElement); //this is how you have to tell the renderer what to display in Vue3

      this.renderer.setPixelRatio(window.devicePixelRatio);
      this.renderer.setSize(window.innerWidth, window.innerHeight);

      this.camera.position.setZ(30);

      this.geometry = new THREE.TorusGeometry(10, 3, 16, 100);
      this.material = new THREE.MeshStandardMaterial({
        color: "purple",
      }); //mesh basic doesn't require a light source to be visible

      this.torusMesh = new THREE.Mesh(this.geometry, this.material);
      this.scene.add(this.torusMesh);
      const pointLight = new THREE.PointLight("white");
      pointLight.position.set(20, 20, 20);
      const ambientLight = new THREE.AmbientLight("white"); //ambientLight is like a 'floodlight', ligths up whole room
      //const lightHelper = new THREE.PointLightHelper(pointLight); //will display the location of a PointLight in the UI as a wireframe; good for positioning a point light
      const gridHelper = new THREE.GridHelper(200, 50);
      this.scene.add(ambientLight, gridHelper);
      this.renderer.render(this.scene, this.camera); // Perform initial rendering operation
      this.controls = new OrbitControls(this.camera, this.renderer.domElement); // Create a control object
      this.animate();
    },
    animate() {
      requestAnimationFrame(this.animate);
      this.torusMesh.rotation.x += 0.01;
      this.torusMesh.rotation.y += 0.01;
      this.torusMesh.rotation.z += 0.01;

      this.controls.update();

      this.renderer.render(this.scene, this.camera);
    },
    moveCamera() {
      console.log("move");
      const currentScrollHeight = document.body.getBoundingClientRect().top; //how far from top of webpage
      this.profileCube.rotation.y += 0.01;
      this.profileCube.rotation.z += 0.01;
      this.camera.z = currentScrollHeight * -0.01;
      this.camera.x = currentScrollHeight * -0.0002;
      this.camera.y = currentScrollHeight * -0.0002;
    },
    addStar() {
      const geometry = new THREE.SphereGeometry(0.25, 24, 24);
      const material = new THREE.MeshStandardMaterial({ color: "white" });
      const star = new THREE.Mesh(geometry, material);

      const [x, y, z] = Array(3)
        .fill()
        .map(() => THREE.MathUtils.randFloatSpread(100)); //generate 3 random numbers between -100 and 100 for the x/y/z values of each star
      star.position.set(x, y, z);
      this.scene.add(star);
    },
    addProfilePic() {
      const myTexture = new THREE.TextureLoader().load(
        require("../assets/profile_img.png")
      );

      const material = new THREE.MeshBasicMaterial({
        map: myTexture,
      });

      this.profileCube = new THREE.Mesh(
        new THREE.BoxGeometry(3, 3, 3),
        material
      );
      this.scene.add(this.profileCube);
    },
  },
};
</script>

<style>
#three-scene {
  top: 0;
  left: 0;
  position: fixed;
  width: 100%;
  height: 100vh;
  overflow: hidden;
}
</style>
