<template>
  <div class="container">
    <div class="top-space"></div> <!-- Üstten boşluk -->

    <h1>Lex Historiae</h1>  <!-- Yeni başlık -->
    <h2 class="subtitle">Ebced Hesaplama Sayfası</h2>

    <!-- Arap Harfleri -->
    <div class="letters">
      <button
        v-for="(value, letter) in ebcedTable"
        :key="letter"
        @click="input += letter"
        class="letter-btn"
      >
        {{ letter }}
      </button>
    </div>

    <!-- Metin Girişi -->
    <textarea
      v-model="input"
      placeholder="Tıklayarak veya klavyeyle Arapça metin girin"
      rows="3"
      class="input-text"
    ></textarea>

    <div class="actions">
      <button @click="clearInput" class="clear-btn">Temizle</button>
    </div>

    <div v-if="input.length" class="results">
      <h2>📜 Harf Değerleri</h2>
      <ul>
        <li v-for="(letter, idx) in letters" :key="idx">
          <span class="letter">{{ letter }}</span> = <b>{{ ebcedTable[letter] || 0 }}</b>
        </li>
      </ul>

      <h2 class="total">Toplam: {{ total }}</h2>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const input = ref('')

const ebcedTable = {
  'ا': 1,  'ب': 2,  'ج': 3,  'د': 4,  'ه': 5,
  'و': 6,  'ز': 7,  'ح': 8,  'ط': 9,  'ي': 10,
  'ك': 20, 'ل': 30, 'م': 40, 'ن': 50, 'س': 60,
  'ع': 70, 'ف': 80, 'ص': 90, 'ق': 100, 'ر': 200,
  'ش': 300,'ت': 400,'ث': 500,'خ': 600,'ذ': 700,
  'ض': 800,'ظ': 900,'غ': 1000
}

const letters = computed(() => input.value.split('').filter(l => l.trim() !== ''))

const total = computed(() => letters.value.reduce((acc, l) => acc + (ebcedTable[l] || 0), 0))

function clearInput() {
  input.value = ''
}
</script>

<style scoped>
.container {
  max-width: 500px;
  margin: 2rem auto;
  padding: 1.5rem;
  border-radius: 12px;
  background: #f9f9fb;
  box-shadow: 0 8px 20px rgb(0 0 0 / 0.1);
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  text-align: center;
  user-select: none;
}

.top-space {
  height: 40px;
}

h1 {
  font-size: 2.4rem;
  color: #1e3a8a;
  margin-bottom: 0.1rem;
  user-select: text;
  font-weight: 700;
}

.subtitle {
  font-size: 1.2rem;
  color: #3b82f6;
  margin-bottom: 1.5rem;
  user-select: text;
  font-weight: 500;
}

.letters {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 0.5rem;
  margin-bottom: 1rem;
}

.letter-btn {
  font-size: 1.3rem;
  background: #e0e7ff;
  border: none;
  border-radius: 6px;
  padding: 0.4rem 0.8rem;
  cursor: pointer;
  transition: background-color 0.25s ease;
  user-select: none;
}

.letter-btn:hover {
  background: #3b82f6;
  color: white;
}

.input-text {
  width: 100%;
  font-size: 1.2rem;
  padding: 0.6rem 0.8rem;
  border-radius: 8px;
  border: 2px solid #d1d5db;
  resize: vertical;
  direction: rtl;
  text-align: right;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

.actions {
  text-align: right;
  margin: 0.7rem 0 1.2rem 0;
}

.clear-btn {
  background-color: #ef4444;
  color: white;
  border: none;
  padding: 0.5rem 1.1rem;
  border-radius: 8px;
  font-weight: 600;
  cursor: pointer;
  user-select: none;
  transition: background-color 0.3s ease;
}

.clear-btn:hover {
  background-color: #b91c1c;
}

.results {
  text-align: left;
  background: white;
  border-radius: 12px;
  padding: 1rem 1.3rem;
  box-shadow: 0 4px 10px rgb(0 0 0 / 0.07);
}

.results h2 {
  color: #2563eb;
  margin-bottom: 0.8rem;
  font-weight: 700;
}

.results ul {
  max-height: 180px;
  overflow-y: auto;
  padding-left: 1rem;
  margin-bottom: 1rem;
}

.results li {
  margin-bottom: 0.3rem;
  font-size: 1.1rem;
}

.letter {
  font-family: monospace;
  font-size: 1.3rem;
  color: #1e40af;
  margin-right: 0.5rem;
}

.total {
  font-size: 1.6rem;
  font-weight: 700;
  color: #1e3a8a;
  text-align: right;
  user-select: text;
}
</style>
