# Boilerplate Vue3 startup code
// // 1, application scenario * /
      // // 1. Create a scene
      // this.scene = new THREE.Scene();
      // // Create a model, something to display
      // // (1). Create a cube geometric object Geometry
      // var geometry = new THREE.BoxGeometry(100, 100, 100);
      // // (2). Creating a material is the layer of the surface of the cube, which is set to blue
      // var material = new THREE.MeshLambertMaterial({
      //   color: 0x0000ff,
      // });
      // // (3). Creating a mesh model object using the just defined (a cube with blue)
      // var mesh = new THREE.Mesh(geometry, material);
      // // 2. Add mesh model (cube) to the scene
      // this.scene.add(mesh);

      // // Second, add light source * /
      // // White light source
      // var point = new THREE.PointLight(0xffffff);
      // // Point light source position
      // point.position.set(400, 200, 300);
      // // Point light source is added to the scene
      // this.scene.add(point);
      // // Environmental light
      // var ambient = new THREE.AmbientLight(0x444444);
      // this.scene.add(ambient);
      // // 3, camera settings
      // var width = window.innerWidth; // Window width
      // var height = window.innerHeight; // Window height
      // var k = width / height; // Window aspect ratio
      // var s = 200; // 3D scene display range control coefficient, the larger the coefficient, the greater the display
      // // Create a camera object
      // this.camera = new THREE.OrthographicCamera(-s * k, s * k, s, -s, 1, 1000);

      // this.camera.position.set(200, 300, 200); // Set camera location
      // this.camera.lookAt(this.scene.position); // Set the camera direction (pointing to the scene object)
      // //Four, camera settings
      // this.renderer = new THREE.WebGLRenderer();
      // this.renderer.setSize(width, height); // Set the rendering area size
      // this.renderer.setClearColor(0xb9d3ff, 1); // Set background color
      // document
      //   .getElementById("three-scene")
      //   .appendChild(this.renderer.domElement); // Body element inserting a Canvas object
      // this.renderer.render(this.scene, this.camera); // Perform rendering operation



# --personal notes

    this.material = new THREE.MeshBasicMaterial({
        color: "red",
        wireframe: true,
      }); //mesh basic doesn't require a light source to be visible


# --LOADING LOCAL IMAGES AS TEXTURES
Could not load local images as textures to apply to geometry. Fix below.

StackOverflow answer:
It works fine when I am loading the texture as an external onlineresource

This does not work for me because of the browser's CORS policy. Chrome's browser console says:

Access to image at 'https://vuejs.org/images/logo.png' from origin 'http://localhost:8080' has been blocked by CORS policy: No 'Access-Control-Allow-Origin' header is present on the requested resource.

Try it with this code instead:

this.myTexture = new THREE.TextureLoader().load(
    require( "../assets/logo.png" )
);

const material = new THREE.MeshBasicMaterial({
    map: this.myTexture,
    alphaTest: 0.5
});