<script setup lang="ts">
import { computed, ref } from 'vue'

type Palette = {
  name: string
  mood: string
  label: string
  colors: [string, string, string]
  title: string
  subtitle: string
  number: string
}

const palettes: Palette[] = [
  { name: '櫻花粉 × 奶油', mood: '輕柔明亮的春日午後', label: 'SAKURA', colors: ['#f7cfd8', '#f5a7b8', '#fff8f0'], title: 'soft\nfocus', subtitle: 'A little sweetness for every day', number: '01' },
  { name: '棉花糖粉 × 蜜桃', mood: '甜而不膩的好心情', label: 'CANDY', colors: ['#f2b6c4', '#f2a48f', '#fff0df'], title: 'sweet\nthings', subtitle: 'Small joys, beautifully noticed', number: '02' },
  { name: '玫瑰粉 × 粉紫', mood: '浪漫裡帶一點想像', label: 'ROSE', colors: ['#ee9eae', '#c99bd2', '#ffe7df'], title: 'wild\nheart', subtitle: 'Small rituals, big feelings', number: '03' },
  { name: '藕粉 × 可可', mood: '安靜溫暖的平衡', label: 'BLUSH', colors: ['#e58a9f', '#70414c', '#f8e7dc'], title: 'form &\nfeeling', subtitle: 'The quiet power of good design', number: '04' },
  { name: '蜜桃粉 × 奶油', mood: '溫暖又有趣的午後', label: 'PEACH', colors: ['#d98298', '#eea68f', '#fff0cf'], title: 'good\ncompany', subtitle: 'A guide to lovely afternoons', number: '05' },
  { name: '裸粉 × 鼠尾草', mood: '復古而柔和的日常', label: 'VINTAGE', colors: ['#c98291', '#a9b39a', '#fff0cf'], title: 'good\ntaste', subtitle: 'An edible kind of optimism', number: '06' },
  { name: '珊瑚粉 × 天藍', mood: '海風裡的輕快心情', label: 'CORAL', colors: ['#c86f85', '#9bd5e2', '#fff1d2'], title: 'sunny\nside', subtitle: 'Notes from a bright place', number: '07' },
  { name: '莓果粉 × 金色', mood: '成熟而有光澤的魅力', label: 'BERRY', colors: ['#bd5d78', '#e6bd67', '#ffe0bd'], title: 'after\nhours', subtitle: 'Stories for the softer hours', number: '08' },
  { name: '螢光粉 × 檸檬黃', mood: '明亮的叛逆感', label: 'NEON', colors: ['#b84c7d', '#f2d64e', '#fff6dd'], title: 'make\nnoise', subtitle: 'The playful issue', number: '09' },
  { name: '玫瑰紅 × 森林綠', mood: '浪漫裡帶一點勇氣', label: 'ROSEWOOD', colors: ['#b83f62', '#c8d7b8', '#ffe7df'], title: 'brave\nromance', subtitle: 'A little courage in full bloom', number: '10' },
  { name: '櫻桃粉 × 墨黑', mood: '果敢而有份量的夜色', label: 'CHERRY', colors: ['#a52b55', '#27252b', '#fff0df'], title: 'bold\nnotes', subtitle: 'A darker kind of sweetness', number: '11' },
  { name: '深莓紅 × 粉紫', mood: '大膽的夜色宣言', label: 'DEEP BERRY', colors: ['#8e2450', '#c99bd2', '#ffe0bd'], title: 'deep\nafterglow', subtitle: 'Stories for the softer hours', number: '12' },
]

const selected = ref(0)
const palette = computed(() => palettes[selected.value])

function choosePalette(index: number) {
  selected.value = index
}
</script>

<template>
  <main :style="{ '--pink': palette.colors[0], '--accent': palette.colors[1], '--paper': palette.colors[2] }">
    <header>
      <a class="wordmark" href="./" aria-label="Pinkroom home"><i></i>pinkroom</a>
      <p>一場色彩配對遊戲</p>
      <span>12 / 12</span>
    </header>

    <section class="intro">
      <div>
        <p class="kicker">PINK EDITION · 2026</p>
        <h1>粉紅色，<em>不只一種個性。</em></h1>
      </div>
      <p class="instruction">選一組粉紅色搭配，看看它會為一本書或一本雜誌帶來什麼樣的心情。</p>
    </section>

    <section class="playground" aria-label="Pink palette matching game">
      <div class="cover-area">
        <div class="cover-shadow"></div>
        <article class="cover" :key="palette.label">
          <div class="cover-top"><span>{{ palette.label }}</span><span>VOL. {{ palette.number }}</span></div>
          <div class="cover-art" aria-hidden="true"><i></i><b></b><strong></strong></div>
          <div class="cover-copy">
            <p>{{ palette.subtitle }}</p>
            <h2>{{ palette.title }}</h2>
          </div>
          <div class="cover-bottom"><span>PINKROOM PRESS</span><span>¥ 980</span></div>
        </article>
        <div class="cover-note"><span></span>{{ palette.mood }}</div>
      </div>

      <aside class="palette-panel">
        <p class="panel-label">MATCH A MOOD · 淺 → 深</p>
        <div class="palette-list" role="radiogroup" aria-label="選擇色彩組合">
          <button v-for="(item, index) in palettes" :key="item.label" class="palette-choice" :class="{ active: selected === index }" type="button" role="radio" :aria-checked="selected === index" @click="choosePalette(index)">
            <span class="choice-number">{{ String(index + 1).padStart(2, '0') }}</span>
            <span class="choice-dots"><i v-for="color in item.colors" :key="color" :style="{ background: color }"></i></span>
            <span class="choice-name">{{ item.name }}</span>
          </button>
        </div>
        <p class="hint">點擊配對，換一本封面。</p>
      </aside>
    </section>

    <footer><span>粉紅色封面研究室</span><span>每一種搭配，都是一個新故事。</span></footer>
  </main>
</template>
