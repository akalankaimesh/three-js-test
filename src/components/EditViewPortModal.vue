<template>
  <b-modal
    centered
    hide-footer
    size="xl"
    id="edit-view-modal"
    body-class="p-0"
    title="Editor"
  >
    <b-row no-gutters>
      <b-col md="12" class="position-relative">
        <div class="w-100" ref="editorFrame"></div>
      </b-col>
    </b-row>
  </b-modal>
</template>

<script>
import * as THREE from "three";
import { OrbitControls } from "three/examples/jsm/controls/OrbitControls";
let camera, scene, renderer;
let mesh;
export default {
  data() {
    return {};
  },
  mounted() {
    this.$nextTick(() => {
      setTimeout(() => {
        this.init();
        this.animate();
      }, 1000);
    });
  },
  methods: {
    init() {
      camera = new THREE.OrthographicCamera(100, 100, 100, 100, 1, 1000);
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
      renderer.setSize(
        this.$refs.editorFrame.clientWidth,
        (this.$refs.editorFrame.clientWidth * 9) / 16
      );

      this.$refs.editorFrame.appendChild(renderer.domElement);
      const controls = new OrbitControls(camera, renderer.domElement);
      controls.target.set(1, 2, 3);
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

      renderer.setSize(
        this.$refs.editorFrame.clientWidth,
        (this.$refs.editorFrame.clientWidth * 9) / 16
      );
      renderer.render(scene, camera);
    },
    animate() {
      requestAnimationFrame(this.animate);
      //mesh.rotation.x += 0.005;
      //mesh.rotation.y += 0.01;
      renderer.render(scene, camera);
    },
  },
};
</script>

<style>
</style>