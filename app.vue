<template>
  <br v-for="x in 3" :key="x"/>

  <div class="container dark-theme">
    <h1>Lex Historiae</h1>
    <h2 class="subtitle">Ebced Hesaplama Sayfası</h2>

    <div class="letters">
      <button
        v-for="letter in arabicAlphabet"
        :key="letter"
        @click="input += letter"
        class="letter-btn"
      >
    {{ letter }}
  </button>
    </div>

    <textarea
      v-model="input"
      placeholder="Tıklayarak veya klavyeyle Arapça metin girin"
      rows="2"
      class="input-text"
    ></textarea>

    <div class="actions">
      <button @click="clearInput" class="clear-btn">Temizle</button>
    </div>

    <div v-if="input.length" class="results-wrapper">
      <div class="results">
        <h2>📜 Harf Değerleri</h2>
        <ul>
          <li v-for="(letter, idx) in letters" :key="idx">
            <span class="letter">{{ letter }}</span> = <b>{{ ebcedTable[letter] || 0 }}</b>
          </li>
        </ul>
      </div>
      <div class="total">
        Toplam: {{ total }}
      </div>
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

const arabicAlphabet = [
  'ا','ب','ت','ث','ج','ح','خ','د','ذ','ر',
  'ز','س','ش','ص','ض','ط','ظ','ع','غ','ف',
  'ق','ك','ل','م','ن','ه','و','ي'
]

const letters = computed(() => input.value.split('').filter(l => l.trim() !== ''))
const total = computed(() => letters.value.reduce((acc, l) => acc + (ebcedTable[l] || 0), 0))

function clearInput() {
  input.value = ''
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Source+Code+Pro:wght@400;600&display=swap');

html, body {
  height: 100%;
  margin: 0;
  padding: 0;
  background-color: #111827;
  color: #e5e7eb;
  font-family: 'Source Code Pro', 'Monaco', 'Consolas', monospace;
}

#app {
  min-height: 100vh;
  background-color: #111827;
}

* {
  box-sizing: border-box;
}

.container {
  max-width: 720px;
  margin: 0 auto;
  padding: 4rem 2rem 3rem;
  background: #1f2937;
  border-radius: 14px;
  box-shadow: 0 10px 28px rgba(0, 0, 0, 0.5);
  text-align: center;
  user-select: none;
}

h1 {
  font-size: 2.6rem;
  color: #60a5fa;
  margin-bottom: 0.15rem;
  user-select: text;
  font-weight: 700;
}

.subtitle {
  font-size: 1.3rem;
  color: #93c5fd;
  margin-bottom: 1.8rem;
  user-select: text;
  font-weight: 600;
  letter-spacing: 0.02em;
}

.letters {
  display: flex;
  flex-wrap: wrap;
  flex-direction: row-reverse;    /* Sağdan sola yazım */
  justify-content: center;        /* 🔥 Ortala */
  gap: 0.6rem;
  margin-bottom: 1.4rem;
}

.letter-btn {
  font-size: 1.4rem;
  background: #374151;
  border: none;
  border-radius: 8px;
  padding: 0.5rem 1rem;
  cursor: pointer;
  transition: background-color 0.3s ease, color 0.3s ease;
  user-select: none;
  box-shadow: 0 2px 5px rgb(59 130 246 / 0.2);
  color: #e5e7eb;
}

.letter-btn:hover {
  background: #2563eb;
  color: white;
  box-shadow: 0 5px 15px rgb(59 130 246 / 0.5);
}

.input-text {
  width: 100%;
  font-size: 1.25rem;
  padding: 0.7rem 1rem;
  border-radius: 12px;
  border: 2px solid #374151;
  resize: vertical;
  direction: rtl;
  text-align: right;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  background-color: #111827;
  color: white;
  box-shadow: inset 0 1px 3px rgb(0 0 0 / 0.05);
  transition: border-color 0.3s ease;
}

.input-text:focus {
  outline: none;
  border-color: #3b82f6;
  box-shadow: 0 0 10px rgb(59 130 246 / 0.4);
}

.actions {
  text-align: right;
  margin: 0.8rem 0 1.5rem 0;
}

.clear-btn {
  background-color: #b91c1c;
  color: white;
  border: none;
  padding: 0.55rem 1.3rem;
  border-radius: 10px;
  font-weight: 700;
  cursor: pointer;
  user-select: none;
  transition: background-color 0.25s ease;
  box-shadow: 0 4px 12px rgb(185 28 28 / 0.5);
}

.clear-btn:hover {
  background-color: #991b1b;
  box-shadow: 0 6px 18px rgb(185 28 28 / 0.7);
}

.results-wrapper {
  background: #1e293b;
  border-radius: 14px;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.5);
  overflow: hidden;
  margin-bottom: 1.5rem;
  text-align: left;
}

.results {
  max-height: 210px;
  overflow-y: auto;
  padding: 1.4rem 1.6rem 0.8rem;
}

.results h2 {
  color: #60a5fa;
  margin-bottom: 1rem;
  font-weight: 700;
  font-size: 1.4rem;
}

.results ul {
  padding-left: 1.1rem;
  margin-bottom: 0;
}

.results li {
  margin-bottom: 0.35rem;
  font-size: 1.15rem;
  color: #e5e7eb;
}

.letter {
  font-family: monospace;
  font-size: 1.5rem;
  color: #93c5fd;
  margin-right: 0.7rem;
  user-select: text;
}

.total {
  font-size: 1.6rem;
  font-weight: 700;
  color: #93c5fd;
  text-align: right;
  padding: 0.9rem 1.6rem 1rem;
  background: #0f172a;
  border-top: 1px solid #334155;
  user-select: text;
}

/* Mobil uyumluluk */
@media (max-width: 768px) {
  .container {
    max-width: 95vw;
    padding: 1.5rem 1.5rem;
  }

  h1 {
    font-size: 2rem;
  }

  .subtitle {
    font-size: 1.1rem;
    margin-bottom: 1.2rem;
  }

  .letters {
    gap: 0.4rem;
  }

  .letter-btn {
    font-size: 1.1rem;
    padding: 0.4rem 0.8rem;
  }

  .input-text {
    font-size: 1.1rem;
    padding: 0.5rem 0.8rem;
  }

  .actions {
    margin: 0.6rem 0 1rem 0;
  }

  .clear-btn {
    padding: 0.45rem 1rem;
    font-size: 0.95rem;
  }

  .results {
    padding: 1rem 1.2rem 0.5rem;
  }

  .results h2 {
    font-size: 1.2rem;
  }

  .results li {
    font-size: 1rem;
  }

  .letter {
    font-size: 1.2rem;
    margin-right: 0.5rem;
  }

  .total {
    font-size: 1.4rem;
    padding: 0.8rem 1.2rem;
  }
}
</style>
