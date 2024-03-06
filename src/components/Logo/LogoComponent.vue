<template>
  <div ref="mount" class="model"></div>
</template>

<script setup>
import { onMounted, ref } from "vue";
import * as THREE from "three";
import { GLTFLoader } from "three/examples/jsm/loaders/GLTFLoader";
import { OrbitControls } from "three/addons/controls/OrbitControls.js";

const mount = ref(null);

onMounted(async () => {
  const scene = new THREE.Scene();
  const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
  const renderer = new THREE.WebGLRenderer({ alpha: true, antialias: true });


  renderer.setSize(window.innerWidth, window.innerHeight);
  mount.value.appendChild(renderer.domElement);

  const loader = new GLTFLoader();
  const gltf = await loader.loadAsync("/models/ThomasGrare.gltf");

  const material = new THREE.MeshBasicMaterial({ color: 0xEDEEF1});

  gltf.scene.traverse((node) => {
    if (node.isMesh) {
      node.material = material;
    }
  });

  scene.add(gltf.scene);

  const controls = new OrbitControls(camera, renderer.domElement);

  camera.position.z = 6;

  const animate = () => {
    requestAnimationFrame(animate);
    controls.update();
    gltf.scene.rotation.y += 0.01;
    renderer.render(scene, camera);
  };

  animate();
});
</script>