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
import moon from "../assets/bbb.jpg";
import ddd from "../assets/aaa.jpg";

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
        alpha: true //透明背景色
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
        60,
        this.width / this.height,
        1,
        10000
      );
      camera.position.z = 10000;
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
      let loader = new THREE.TextureLoader();
      let group = new THREE.Group();
      /*材质 纹理加载器*/
      loader.load(
        moon,
        texture => {
          for (let i = 0; i < 10; i++) {
            for (let j = 0; j < 10; j++) {
              let geometry = new THREE.BoxBufferGeometry(100, 10, 100, 1, 2, 2);
              let material = new THREE.MeshBasicMaterial({ map: texture });
              let circle = new THREE.Mesh(geometry, material);
              circle.position.set(i * 100, 0, j * 100);
              group.add(circle);
            }
          }

          for (let i = 0; i < 10; i++) {
            for (let j = 0; j < 10; j++) {
              let geometry = new THREE.BoxBufferGeometry(10, 100, 100, 1, 2, 2);
              let material = new THREE.MeshBasicMaterial({ map: texture });
              let circle = new THREE.Mesh(geometry, material);
              circle.position.set(-50, 100 * i + 50, j * 100);
              group.add(circle);
            }
          }
          for (let i = 0; i < 10; i++) {
            for (let j = 0; j < 10; j++) {
              let geometry = new THREE.BoxBufferGeometry(10, 100, 100, 1, 2, 2);
              let material = new THREE.MeshBasicMaterial({ map: texture });
              let circle = new THREE.Mesh(geometry, material);
              circle.position.set(1000 - 50, 100 * i + 50, j * 100);
              group.add(circle);
            }
          }
          scene.add(group);
        },
        xhr => {},
        err => {}
      );
      loader.load(
        ddd,
        texture => {
          for (let i = 0; i < 10; i++) {
            for (let j = 0; j < 10; j++) {
              let geometry = new THREE.BoxBufferGeometry(10, 100, 100, 1, 2, 2);
              let material = new THREE.MeshBasicMaterial({ map: texture });
              let circle = new THREE.Mesh(geometry, material);
              circle.position.set(
                1200 - i * Math.sqrt((100 * 100) / 2),
                Math.sqrt((100 * 100) / 2) * i +
                  (1100 - Math.sqrt((490 * 490) / 2)),
                j * 100
              );
              circle.rotation.z = -15;
              group.add(circle);
            }
          }
          for (let i = 0; i < 10; i++) {
            for (let j = 0; j < 10; j++) {
              let geometry = new THREE.BoxBufferGeometry(10, 100, 100, 1, 2, 2);
              let material = new THREE.MeshBasicMaterial({ map: texture });
              let circle = new THREE.Mesh(geometry, material);
              circle.position.set(
                -300 + i * Math.sqrt((100 * 100) / 2),
                Math.sqrt((100 * 100) / 2) * i +
                  (1100 - Math.sqrt((490 * 490) / 2)),
                j * 100
              );
              circle.rotation.z = 15;
              group.add(circle);
            }
          }
          scene.add(group);
        },
        xhr => {},
        err => {}
      );
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
