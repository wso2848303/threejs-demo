<template>
  <div class="home" id="page"></div>
</template>

<script setup>
import { onMounted } from "@vue/runtime-core";
import * as THREE from "three";
const scene = new THREE.Scene();
const camera = new THREE.PerspectiveCamera(
  75,
  window.innerWidth / window.innerHeight,
  0.1,
  1000
);
const light = new THREE.AmbientLight(0x404040); // soft white light
scene.add(light);
const renderer = new THREE.WebGLRenderer();
renderer.setSize(window.innerWidth, window.innerHeight);
document.body.appendChild(renderer.domElement);
camera.position.z = 5;
onMounted(() => {
  initCube();
  // function animate() {
  //   // requestAnimationFrame(animate);

  // }
  // animate();
  // renderer.render(scene, camera);
});
const initCube = () => {
  const geometry = new THREE.BoxGeometry(1, 1, 1);
  const material = new THREE.MeshBasicMaterial({ color: 0x00ff00 });
  const cube = new THREE.Mesh(geometry, material);
  scene.add(cube);
  const animate = () => {
    cube.rotation.x += 0.01;
    cube.rotation.y += 0.01;
    requestAnimationFrame(animate);
    renderer.render(scene, camera);
  };
  animate();
};
</script>
