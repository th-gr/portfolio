<template>
  <TresCanvas v-bind="gl">
    <TresPerspectiveCamera :position="[0.6, 0.2, 0.4]" :look-at="[0, 2, 0]" />
    <OrbitControls />
    <Suspense>
      <LogoComponent></LogoComponent>
    </Suspense>
    <TresDirectionalLight :position="[3, 3, 3]" :intensity="1" />
    <TresAmbientLight :intensity="2" />
  </TresCanvas>
</template>
  
<script setup>
import { TresCanvas } from "@tresjs/core";
import { OrbitControls } from "@tresjs/cientos";
import { BasicShadowMap, SRGBColorSpace, NoToneMapping } from "three";
import LogoComponent from "./LogoComponent.vue";
// import { onMounted } from "vue";

const gl = {
  clearColor: "#F78B3D",
  shadows: true,
  alpha: false,
  shadowMapType: BasicShadowMap,
  outputColorSpace: SRGBColorSpace,
  toneMapping: NoToneMapping,
  windowSize: true,
};
</script>