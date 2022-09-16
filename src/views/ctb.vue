<template>
  <div></div>
</template>
<script setup>
import { onMounted } from "@vue/runtime-core";
import * as THREE from "three";
import { GLTFLoader } from "three/examples/jsm/loaders/GLTFLoader";
const renderer = new THREE.WebGLRenderer();
renderer.setSize(window.innerWidth, window.innerHeight);
document.body.appendChild(renderer.domElement);
const scene = new THREE.Scene();
const camera = new THREE.PerspectiveCamera(
  75,
  window.innerWidth / window.innerHeight
);
const light = new THREE.AmbientLight(0xffffff);
scene.add(light);
onMounted(() => {
  const loader = new GLTFLoader();
  loader.load(
    // "/yellow-plaster-3d-model/yellow_plaster_4k.gltf",
    "/CTB-gltf-demo.gltf",
    // "/free_1975_porsche_911_930_turbo/scene.gltf",
    function (gltf) {
      console.log(gltf);
      scene.add(gltf.scene);
      console.log(scene);
      gltf.animations; // Array<THREE.AnimationClip>
      gltf.scene; // THREE.Group
      gltf.scenes; // Array<THREE.Group>
      gltf.cameras; // Array<THREE.Camera>
      gltf.asset; // Object
      renderer.render(scene, camera);
    },
    function (xhr) {
      console.log((xhr.loaded / xhr.total) * 100 + "% loaded");
    },
    function (error) {
      console.error(error);
    }
  );
  // renderer.render(scene, camera);
});
</script>
