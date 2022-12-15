<template>
  <b-row>
    <b-col>Test</b-col>
  </b-row>
</template>

<script>
import * as THREE from "three";
let camera, scene, renderer;
let mesh;
export default {
  data() {
    return {};
  },
  mounted() {
    this.$nextTick(() => {
      this.init();
      this.animate();
    });
  },
  methods: {
    init() {
      camera = new THREE.PerspectiveCamera(
        70,
        window.innerWidth / window.innerHeight,
        1,
        1000
      );
      camera.position.z = 400;

      scene = new THREE.Scene();

      const texture = new THREE.TextureLoader().load(
        require("../assets/texture.jpg")
      );

      const geometry = new THREE.BoxGeometry(200, 200, 200);
      const material = new THREE.MeshBasicMaterial({ map: texture });

      mesh = new THREE.Mesh(geometry, material);
      scene.add(mesh);

      renderer = new THREE.WebGLRenderer({ antialias: true });
      renderer.setPixelRatio(window.devicePixelRatio);
      renderer.setSize(window.innerWidth, window.innerHeight);
      document.body.appendChild(renderer.domElement);

      //

      window.addEventListener("resize", this.onWindowResize);
    },
    onWindowResize() {
      camera.aspect = window.innerWidth / window.innerHeight;
      camera.updateProjectionMatrix();

      renderer.setSize(window.innerWidth, window.innerHeight);
    },
    animate() {
      requestAnimationFrame(this.animate);

      mesh.rotation.x += 0.005;
      mesh.rotation.y += 0.01;

      renderer.render(scene, camera);
    },
  },
};
</script>

<style>
</style>