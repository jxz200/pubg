<script setup lang="ts">
import { World, Model, ThirdPersonCamera, Dummy, Find, Setup, types, keyboard } from "lingo3d-vue";
import { ref } from "vue";
const dummyRef = ref<types.Dummy>()
console.log(dummyRef);

keyboard.onKeyPress = (key, pressed) => {
  const dummy = dummyRef.value
  if(!dummy) return 
  console.log(pressed);

  if(pressed.has('w')) dummy.strideForward = -10
  if(pressed.has('s')) dummy.strideForward = 10
  if(pressed.has('a')) dummy.strideRight = 10
  if(pressed.has('d')) dummy.strideRight = -10
  if(pressed.has('shift')) dummy.strideForward = dummy.strideForward*3
}
keyboard.onKeyDown = (key) => {
  const dummy = dummyRef.value
  if(!dummy) return
  if(key === 'Space') dummy.jump(5)
}
keyboard.onKeyUp = (key, pressed) => {
  const dummy = dummyRef.value
  if(!dummy) return 
  if(!pressed.has('w') && !pressed.has('s')) dummy.strideForward = 0
  if(!pressed.has('a') && !pressed.has('d')) dummy.strideRight = 0
}
</script>

<template>
  <World>
    <Model
      :metalness-factor="0.7"
      :roughness-factor="0.4"
      :x="43.83"
      :y="54.52"
      :z="157.37"
      :width="121.25"
      :depth="84.17"
      :scale-x="150"
      :scale-y="150"
      :scale-z="150"
      src="map.glb"
      physics="map"
    />
    <ThirdPersonCamera
      :x="-574.08"
      :y="-539.66"
      :z="1679.88"
      :rotation-x="-180"
      :rotation-z="-180"
      :rotation="-180"
      :inner-z="150"
      mouse-control-mode="orbit"
      active
      mouse-control
      :inner-x="20"
    >
      <Dummy
        :animations="{
          idle: 'https://unpkg.com/lingo3d-dummy@1.0.1/assets/rifle-idle.fbx',
          running:
            'https://unpkg.com/lingo3d-dummy@1.0.1/assets/rifle-running.fbx',
          runningBackwards:
            'https://unpkg.com/lingo3d-dummy@1.0.1/assets/rifle-running-backwards.fbx',
          jumping:
            'https://unpkg.com/lingo3d-dummy@1.0.1/assets/rifle-falling.fbx',
        }"
        animation="idle"
        pbr
        :x="-574.08"
        :y="-539.66"
        :z="1679.88"
        :width="20"
        :depth="20"
        src="https://unpkg.com/lingo3d-dummy@1.0.1/assets/ybot.fbx"
        preset="rifle"
        stride-move
        ref="dummyRef"
        physics="character"
      >
        <Find name="mixamorigLeftHand" :normal-scale="{ x: 1, y: 1 }" />
        <Find name="mixamorigRightHand" :normal-scale="{ x: 1, y: 1 }">
          <Model
            outline
            :x="-2771.49"
            :y="-452.6"
            :z="-69.69"
            :width="26.63"
            :depth="277.87"
            :scale-x="36.09"
            :scale-y="36.09"
            :scale-z="36.09"
            :rotation-x="-158.17"
            :rotation-y="-83.98"
            :rotation-z="106.06"
            :rotation="106.06"
            src="gun.glb"
          />
        </Find>
      </Dummy>
    </ThirdPersonCamera>
    <Setup default-light="studio" :default-light-scale="1.2" />
  </World>
</template>
