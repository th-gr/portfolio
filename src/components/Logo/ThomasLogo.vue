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
    <TresAmbientLight :intensity="2" />
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


onLoop(({ delta, elapsed }) => {
  if (boxRef.value) {
    boxRef.value.rotation.y += delta;
    boxRef.value.rotation.z = elapsed * 0.2;
  }
});

const gl = {

  shadows: true,
  alpha: false,
  shadowMapType: BasicShadowMap,
  outputColorSpace: SRGBColorSpace,
  toneMapping: NoToneMapping,
  windowSize: true,
};
</script>