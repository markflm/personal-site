<template>
  <div id="three-scene"></div>
</template>

<script>
import * as THREE from "three";
//import { OrbitControls } from "three/examples/jsm/controls/OrbitControls";
export default {
  name: "Scene",
  props: {
    showAnimation: {
      type: Boolean,
      default: true,
    },
  },
  data() {
    return {};
  },
  mounted() {
    //window.addEventListener("scroll", this.moveCamera);
    this.init();
    //this.addProfilePic();
  },
  unmounted() {
    //window.removeEventListener("scroll", this.moveCamera);
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

      this.camera.position.z = 30;

      this.renderer = new THREE.WebGLRenderer();
      document
        .getElementById("three-scene")
        .appendChild(this.renderer.domElement); //this is how you have to tell the renderer what to display in Vue3

      this.renderer.setPixelRatio(window.devicePixelRatio);
      this.renderer.setSize(window.innerWidth, window.innerHeight);
      const pointLight = new THREE.PointLight("purple");
      pointLight.position.set(30);
      const ambientLight = new THREE.AmbientLight("purple"); //ambientLight is like a 'floodlight', ligths up whole room
      const lightHelper = new THREE.PointLightHelper(pointLight); //will display the location of a PointLight in the UI as a wireframe; good for positioning a point light

      const geometry = new THREE.TorusGeometry(10, 3, 16, 100);
      const material = new THREE.MeshStandardMaterial({
        color: 0xff6347,
        wireframe: true,
      });
      this.torus = new THREE.Mesh(geometry, material);
      this.torus.position.y = 100;
      this.scene.add(pointLight, lightHelper, ambientLight, this.torus);
      this.renderer.render(this.scene, this.camera); // Perform initial rendering operation
      //this.controls = new OrbitControls(this.camera, this.renderer.domElement); // Create a control object
      this.createStarGeometry();
      this.camera.lookAt(0, 75, 0); //make camera look up to simulate movement through stars
      this.animate();
    },
    animate() {
      this.starPoints.forEach((x) => {
        x.velocity += x.acceleration;
        x.y -= x.velocity;
        if (x.y < -20) {
          x.y = 30;
          x.velocity = 0;
        }
      });
      this.starGeo.setFromPoints(this.starPoints);
      this.stars.rotation.y += 0.00005;
      requestAnimationFrame(this.animate);

      this.torus.rotation.x += 0.01;
      this.torus.rotation.y += 0.01;
      this.torus.rotation.z += 0.01;
      //this.controls.update();

      this.renderer.render(this.scene, this.camera);
    },
    createStarGeometry() {
      this.starGeo = new THREE.BufferGeometry();
      this.starPoints = [];
      for (let i = 0; i < 3000; i++) {
        let star = new THREE.Vector3(
          THREE.MathUtils.randFloatSpread(100),
          THREE.MathUtils.randFloatSpread(100),
          THREE.MathUtils.randFloatSpread(100)
        );
        star.velocity = 0;
        star.acceleration = 0.00002;
        this.starPoints.push(star);
      }
      this.starGeo.setFromPoints(this.starPoints);
      let texture = new THREE.TextureLoader().load(
        require("../assets/circle.png")
      );
      let starMat = new THREE.PointsMaterial({
        color: "white",
        size: 0.2,
        map: texture,
      });
      this.stars = new THREE.Points(this.starGeo, starMat);
      this.scene.add(this.stars);
    },
    // moveCamera() {
    //   console.log("move");
    //   const currentScrollHeight = document.body.getBoundingClientRect().top; //how far from top of webpage
    //   this.profileCube.rotation.y += 0.01;
    //   this.profileCube.rotation.z += 0.01;
    //   this.camera.z = currentScrollHeight * -0.01;
    //   this.camera.x = currentScrollHeight * -0.0002;
    //   this.camera.y = currentScrollHeight * -0.0002;
    // },
    // addStar() {
    //   const geometry = new THREE.SphereGeometry(0.25, 24, 24);
    //   const material = new THREE.MeshStandardMaterial({ color: "white" });
    //   const star = new THREE.Mesh(geometry, material);

    //   const [x, y, z] = Array(3)
    //     .fill()
    //     .map(() => THREE.MathUtils.randFloatSpread(100)); //generate 3 random numbers between -100 and 100 for the x/y/z values of each star
    //   star.position.set(x, y, z);
    //   this.scene.add(star);
    // },
  },
};
</script>

<style>
#three-scene {
  top: 0;
  left: 0;
  position: fixed;
  width: 100vw;
  height: 100vh;
  overflow: hidden;
  overflow-x: hidden;
}
</style>
