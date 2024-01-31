<template>
  <TresCanvas v-bind="gl" class="canvas">
  <TresPerspectiveCamera :fov="90"/>
    <OrbitControls />
    <TresMesh ref="boxRef" :position="[0, 0, 0]">
      <Suspense>
        <LogoComponent></LogoComponent>
      </Suspense>
      <TresMeshNormalMaterial />
    </TresMesh>
    <TresDirectionalLight :position="[3, 3, 3]" :intensity="1" />
    <TresAmbientLight :intensity="5" />
  </TresCanvas>
</template>
  
<script setup>
import { shallowRef } from "vue";
import { TresCanvas, useRenderLoop } from "@tresjs/core";
import { OrbitControls } from "@tresjs/cientos";
import { BasicShadowMap, SRGBColorSpace, NoToneMapping } from "three";
import LogoComponent from "./LogoComponent.vue";

const boxRef = shallowRef(null);
const { onLoop } = useRenderLoop();


onLoop(() => {
  boxRef.value.rotation.y += 0.01;
});

const gl = {
  "clear-color" : "#504C57",
  shadows: true,
  alpha: false,
  shadowMapType: BasicShadowMap,
  outputColorSpace: SRGBColorSpace,
  toneMapping: NoToneMapping,
  windowSize: true,
};
</script>