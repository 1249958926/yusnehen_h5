<template><div></div></template>
<script lang="ts" setup>
import * as PIXI from 'pixi.js'
import * as PIXI_SPINE from 'pixi-spine'
import gsap from 'gsap'
import { ref } from 'vue';
let loadCount = 0
const app = new PIXI.Application({
  width: 1920,
  height: 6000,
  backgroundColor: 0x1099bb,
  resolution: window.devicePixelRatio || 1
});

document.body.appendChild(app.view);
let arr = [
  './spine/kong.json',
  './spine/paimeng.json',
  './spine/ying.json',
  './spine/keli.json'
]
// load spine data
arr.forEach((item, index) => {
  PIXI.Assets.load(item).then(onAssetsLoaded);
})
function onAssetsLoaded(spineboyAsset) {
  //每调用一次+1
  loadCount += 1
  app.stage.interactive = true;

  // create a spine boy
  const spineBoy = new PIXI_SPINE.Spine(spineboyAsset.spineData);

  // set the position
  spineBoy.x = 200 + 350 * (loadCount % 4);
  spineBoy.y = 600 * Math.ceil(loadCount / 4);

  spineBoy.scale.set(0.5);

  // play animation
  spineBoy.state.setAnimation(0, 'animation', true);
  // spineBoy.state.setAnimation(0, 'extra', true);

  app.stage.addChild(spineBoy);

  // gsap.from(spineBoy, { opacity: 0, x: 500, duration: 3.5 })

  app.stage.on('click', () => {
    // spineBoy.state.setAnimation(0, 'animation', false);
    // spineBoy.state.addAnimation(0, 'walk', true, 0);
  });
}

</script>