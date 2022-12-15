<template>
  <b-row no-gutters class="justify-content-center">
    <b-col md="8"><div class="main-frame" ref="mainFrame"></div></b-col>
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
      camera = new THREE.PerspectiveCamera(70, 16 / 9, 1, 1000);
      camera.position.z = 800;

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
      renderer.setSize(this.$refs.mainFrame.clientWidth, 500);

      this.$refs.mainFrame.appendChild(renderer.domElement);
      mesh.rotation.x += 10;
      mesh.rotation.y += 10;
      setTimeout(() => {
        this.onWindowResize();
      }, 1000);
      window.addEventListener("resize", this.onWindowResize);
    },
    onWindowResize() {
      camera.aspect = 16 / 9;
      camera.updateProjectionMatrix();

      renderer.setSize(this.$refs.mainFrame.clientWidth, 500);
      renderer.render(scene, camera);
    },
    animate() {
      //requestAnimationFrame(this.animate);
      //mesh.rotation.x += 0.005;
      //mesh.rotation.y += 0.01;
    },
  },
};
</script>

<style>
.main-frame {
  width: 100%;
}
</style>