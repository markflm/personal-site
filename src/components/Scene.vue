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
    window.addEventListener("resize", this.resizeCanvas);
    this.init();
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

      //this.camera.position.z = 30;

      this.renderer = new THREE.WebGLRenderer();
      document
        .getElementById("three-scene")
        .appendChild(this.renderer.domElement); //this is how you have to tell the renderer what to display in Vue3

      this.renderer.setPixelRatio(window.devicePixelRatio);
      this.renderer.setSize(window.innerWidth, window.innerHeight);
      const pointLight = new THREE.PointLight("pink");

      const geometry = new THREE.TorusKnotGeometry(10, 3, 100, 100);
      const material = new THREE.MeshStandardMaterial({
        color: 0xff6347,
        wireframe: true,
      });
      this.torus = new THREE.Mesh(geometry, material);
      this.torus.position.y = 40;
      this.torus.position.x = 25;
      this.torus.position.z = 15;

      this.scene.add(pointLight, this.torus);
      this.renderer.render(this.scene, this.camera); // Perform initial rendering operation
      this.createStarGeometry();
      this.camera.lookAt(0, 25, 0); //make camera look up to simulate movement through stars
      this.animate();
    },
    animate() {
      this.starPoints.forEach((x) => {
        x.velocity += x.acceleration;
        x.y -= x.velocity;
        if (x.y < -20) {
          x.y = 20;
          x.velocity = 0;
        }
      });
      this.starGeo.setFromPoints(this.starPoints);
      this.stars.rotation.y += 0.00005;
      requestAnimationFrame(this.animate);

      this.torus.rotation.x += 0.001;
      this.torus.rotation.y += 0.001;
      this.torus.rotation.z += 0.001;
      //this.torus.position.x -= 0.01;

      //console.log(this.torus.position);

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
        star.acceleration = 0.0001;
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
    resizeCanvas() {
      this.camera.aspect = window.innerWidth / window.innerHeight;
      this.camera.updateProjectionMatrix();
      this.renderer.setPixelRatio(window.devicePixelRatio);
      this.renderer.setSize(window.innerWidth, window.innerHeight);
      //this.animate();
    },
    // moveCamera() {
    //   console.log("move");
    //   const currentScrollHeight = document.body.getBoundingClientRect().top; //how far from top of webpage
    //   // this.profileCube.rotation.y += 0.01;
    //   // this.profileCube.rotation.z += 0.01;
    //   this.camera.position.z += currentScrollHeight * 0.1;
    //   this.camera.position.x += currentScrollHeight * 0.001;
    //   this.camera.position.y += currentScrollHeight * 0.0002;
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
}
</style>
