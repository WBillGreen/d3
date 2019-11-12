<template>
  <div class="container">
    <div ref="d3Wrap"></div>
  </div>
</template>

<script>
import * as THREE from "three";
import Stats from "three/examples/jsm/libs/stats.module";
import { OrbitControls } from "three/examples/jsm/controls/OrbitControls";
// import { GLTFLoader } from "three/examples/jsm/loaders/GLTFLoader";
// import { DRACOLoader } from "three/examples/jsm/loaders/DRACOLoader";
let stats, renderer, scene, camera, directionalLight;
export default {
  name: "home",
  data() {
    return {
      width: window.innerWidth,
      height: window.innerHeight
    };
  },
  methods: {
    initRenderer() {
      stats = new Stats();
      this.$refs.d3Wrap.appendChild(stats.dom);

      renderer = new THREE.WebGLRenderer({
        alpha: true
      });
      renderer.setSize(this.width, this.height);
      this.$refs.d3Wrap.appendChild(renderer.domElement);
    },
    initScene() {
      scene = new THREE.Scene();
      new OrbitControls(camera, renderer.domElement);
    },
    initCamera() {
      camera = new THREE.PerspectiveCamera(
        30,
        this.width / this.height,
        0.1,
        100
      );
      camera.position.z = 100;
    },
    initLight() {
      directionalLight = new THREE.DirectionalLight(0xffffff, 0.5);
      directionalLight.position.set(0, 1, 0);
      scene.add(directionalLight);
    },
    initCircle() {
      let geometry = new THREE.CircleBufferGeometry(5, 32);
      let material = new THREE.MeshBasicMaterial({ color: 0xff0011 });
      let circle = new THREE.Mesh(geometry, material);
      scene.add(circle);
    },
    initCone() {
        var geometry = new THREE.BoxBufferGeometry( 1, 1, 2,1,2,2 );
        var material = new THREE.MeshBasicMaterial( {color: 0xffdd22} );
        var cube = new THREE.Mesh( geometry, material );
        scene.add( cube );
    },
    render() {
      requestAnimationFrame(this.render);
      stats.update();
      renderer.render(scene, camera);
    }
  },
  mounted() {
    this.initRenderer();
    this.initCamera();
    this.initScene();
    this.initLight();
    // this.initCircle();
    this.initCone();
    this.render();
  }
};
</script>
<style lang="scss" scoped>
.container {
}
</style>
