<template>
  <primitive :object="scene" />
</template>

<script setup>
import { useLoader } from "@tresjs/core";
import { GLTFLoader } from "three/addons/loaders/GLTFLoader";

const { scene } = await useLoader(GLTFLoader, "/models/logo_tg.gltf");

</script>