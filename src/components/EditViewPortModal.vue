<template>
  <b-modal
    @shown="init(), animate()"
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
    return {
      controls: null,
    };
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
      let clientWidth = this.$refs.editorFrame.clientWidth;
      camera = new THREE.OrthographicCamera(
        -clientWidth / 2,
        clientWidth / 2,
        -(clientWidth / 2),
        clientWidth / 2,
        -1000,
        1000
      );
      //camera.position.z = 800;

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
      this.controls = new OrbitControls(camera, renderer.domElement);
      this.controls.target.set(1, 1, 1);
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
  watch: {
    controls(data) {
      console.log(data);
    },
  },
};
</script>

<style>
</style>