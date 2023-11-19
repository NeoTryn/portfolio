<script setup lang="ts">
//import NavBar from './components/NavBar.vue'

import * as three from 'three'
import { MeshBasicMaterial, SphereGeometry } from 'three/src/Three.js';
import { onMounted, ref } from 'vue'

const bg = ref<HTMLCanvasElement | null>(null);

const scene = new three.Scene();
const camera = new three.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
scene.add(camera);
camera.position.z = 5;

const sphere = new three.Mesh(
  new SphereGeometry(1, 20, 20),
  new MeshBasicMaterial({ color: 0x008080 }),
);
scene.add(sphere);

onMounted(() => {
  //renderer.render(scene, camera);
  const renderer = new three.WebGLRenderer({
    canvas: bg.value!,
    antialias: true,
  });

  renderer.setSize(window.innerWidth, window.innerHeight);

  window.addEventListener('resize', () => {
    const newWidth = window.innerWidth;
    const newHeight = window.innerHeight;

    camera.aspect = newWidth / newHeight;
    camera.updateProjectionMatrix();

    renderer.setSize(newWidth, newHeight);
  });

  const animate = () => {
    requestAnimationFrame(animate);
    renderer.render(scene, camera);
  }
  animate();
});
//
</script>

<template>
  <canvas ref="bg" id="bg"/>
</template>

<style>
  @import url('./Background.scss');
</style>