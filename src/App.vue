<template>
  <div>

</div>
</template>
<script setup lang="ts">
// 导入pixi.js
import * as PIXI from 'pixi.js'
// 创建应用
const app = new PIXI.Application({
  width: window.innerWidth,
  height: window.innerHeight,
  backgroundColor: 0x1099bb,
  resolution: window.devicePixelRatio || 1
})
// 将应用画布添加到DOM中
document.body.appendChild(app.view);

// 创建一个矩形
const rectangle = new PIXI.Graphics();
rectangle.beginFill(0x66ccff, 0.1) // 填充颜色
rectangle.drawRect(0, 0, 64, 64) // 绘制矩形
rectangle.endFill() // 结束填充
// 将矩形添加到舞台
app.stage.addChild(rectangle)
// 图形的缩放
rectangle.scale.set(2, 2)

// 创建一个纹理
const texture = PIXI.Texture.from('./textures/jian.png')

// 创建一个精灵
const sprite = new PIXI.Sprite(texture);
// 设置精灵的位置
sprite.x = app.screen.width / 2;
sprite.y = app.screen.height / 2;
app.stage.addChild(sprite)
// 设置精灵的锚点
sprite.anchor.set(0.5, 0.5)
// ticker实现动画
app.ticker.add((delta) => {
  sprite.rotation += 0.01 * delta
})
// 给精灵添加点击事件
sprite.interactive = true // 打开交互事件
sprite.on('click', () => {
  console.log('click');
})

// 添加资源
PIXI.Assets.add('jian', './textures/jian.png')
PIXI.Assets.add('avatar', './textures/avatar.png')
PIXI.Assets.add('shu', './textures/shu.png')
// 异步加载资源
const texturesPromise = PIXI.Assets.load(['jian', 'avatar', 'shu'])

</script>