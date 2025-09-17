<template>
  <div id="app">
    <h1>Vue Beispiele</h1>
    <div class="grid">
      <!-- Jede Aufgabe in einem Block -->
      <section class="card">
        <h2>Mein Counter</h2>
        <p class="green">Wert: {{ counter }}</p>
        <button @click="counter++">+</button>
        <button @click="counter--">-</button>
        <button @click="reset">Reset</button>
      </section>

      <section class="card">
        <h2>Toggle mit Transition</h2>
        <button @click="exists = !exists">{{ btnText }}</button>
        <Transition>
          <p v-if="exists">Hello World!</p>
        </Transition>
      </section>

      <section class="card">
        <h2>v-else</h2>
        <button @click="word = 'pizza'">Word = 'Pizza'</button>
        <div v-if="word === 'apple'"><p class="green">Apple</p></div>
        <div v-else-if="word === 'pizza'"><p class="green">Pizza</p></div>
      </section>

      <section class="card">
        <h2>Text includes</h2>
        <div v-if="text.includes('pizza')">
          <p class="green">Text enthält 'pizza'</p>
        </div>
        <div v-else-if="text.includes('burrito')">
          <p class="green">Text enthält 'burrito'</p>
        </div>
        <p v-else class="green">Text enthält weder 'pizza' noch 'burrito'</p>
      </section>

      <section class="card">
        <h2>Bildwechsel</h2>
        <button @click="nextImg">Next image</button>
        <Transition mode="out-in">
          <img
            v-if="imgActive === 'pizza'"
            src="/assets/OIP.jpg"
            :key="'pizza'"
          />
          <img
            v-else-if="imgActive === 'cake'"
            src="/assets/cake.jpg"
            :key="'cake'"
          />
          <img
            v-else-if="imgActive === 'fish'"
            src="/assets/fish.jpg"
            :key="'fish'"
          />
          <img
            v-else-if="imgActive === 'rice'"
            src="/assets/rice.jpg"
            :key="'rice'"
          />
        </Transition>
      </section>

      <section class="card">
        <h2>v-model Input (lazy + trim) test</h2>
        <input v-model.lazy.trim="inputValue" placeholder="Tippe hier..." />
        <br />
        <p>Value: "{{ inputValue }}"</p>
      </section>

      <section class="card">
        <h2>v-model mit Child</h2>
        <ChildComponentInput
          v-model="parentBananeValue"
          placeholder="Tippe hier..."
        />
        <p>Parent has: "{{ parentBananeValue }}"</p>
      </section>

      <section class="card">
        git init
        <h2>v-on</h2>
        <div v-bind:class="{ yalClass: bgColor }">
          <p>Click the button to change background color of this DIV box.</p>
          <button v-on:click="bgColor = !bgColor">Click</button>
          <p>bgColor property: "{{ bgColor }}"</p>
        </div>
      </section>

      <section class="card">
        <h2>v-on-capture</h2>

        <p>
          When the '.capture' modifier is used on the parent DIV element, the
          event is captured first in the parent element when the child element
          is clicked.
        </p>
        <p>
          If the '.capture' modifier is removed from this code, the child
          element will capture the click event first. This is the default
          behavior, that the event bubbles up, first in child element, then to
          the parent.
        </p>
        <div v-on:click.capture="msg.push('parent')" id="parent">
          <p>This is the parent element.</p>
          <div v-on:click="msg.push('child')">
            <p>This is the child element. CLICK HERE!</p>
          </div>
        </div>
        <p>The order of when and where the event is captured.</p>
        <ol>
          <li v-for="(x, index) in msg" :key="index">{{ x }}</li>
        </ol>
      </section>

      <section class="card">
        <h2>v-on:click.once</h2>
        <p>
          The '.once' modifier prevents the event from happening more than once.
        </p>
        <button v-on:click.once="clickTimes++">Click</button>
        <p>Click event happened {{ clickTimes }} times.</p>
      </section>

      <section class="card">
        <h2>v-on:scroll.passive</h2>
        <p>
          The '.passive' modifier sets the event handler as passive, and this
          can enhance performance.
        </p>
        <div class="scroll" v-on:scroll.passive="scrollTimes++" id="parent">
          <p>Scroll here.</p>
          <p>Bladi-bladi-bladi</p>
          <p>potato potato</p>
          <p>Scroll-scroll-scroll</p>
          <p>Scroll more...</p>
        </div>
        <p>Scroll happended {{ scrollTimes }} times.</p>
      </section>

      <section class="card">
        <h2>v-on:click.left & shift</h2>
        <p>Hold 'Shift' key and press left mouse button on the image:</p>
        <img @click.left="onImgClick" :src="imgUrl" />
      </section>

      <section class="card">
        <h2>JavaScript Transition Hooks</h2>

        <p>
          This code hooks into "after-enter" so that after the initial animation
          is done, a method runs that displays a red div.
        </p>
        <button @click="pVisible = true">Create p-tag!</button><br />
        <Transition @after-enter="onAfterEnter">
          <p v-show="pVisible" id="p1">Hello World!</p>
        </Transition>
        <br />
        <div v-show="divVisible">
          This appears after the "enter-active" phase of the transition.
        </div>
      </section>

      <section class="card">
        <h2>mit SlotComponent</h2>
        <p>
          Die Komponente hat ein &lt;div&gt;-Element mit einem benannten
          &lt;slot&gt;:
          <code>topSlot</code>
        </p>
        <slot-component>
          <template v-slot:topSlot>
            Hello! ich bin Text von SlotElement
          </template>
        </slot-component>
      </section>

      <section class="card">
        <h2>Local Component</h2>
        <p>App.vue controls how local data from the scoped slot is rendered.</p>
        <data-slot-component v-slot="{ dataFromMySlot }">
          <p>{{ dataFromMySlot }}</p>
        </data-slot-component>
      </section>

      <section class="card">
        <h2>Example watch Option</h2>
        <p>
          The 'rangeVal' watcher is written with <code>immediate: true</code>,
          so the value automatically jumps to 70 when the page first loads. If
          you move the slider between 20 and 40, the value will snap to 20. If
          you move it between 40 and 70, the value will snap to 70. Values below
          20 or above 70 will remain unchanged.
        </p>

        <!-- Schieberegler, der direkt mit rangeVal verbunden ist -->
        <input type="range" v-model="rangeVal" />

        <!-- Anzeige vom aktuellen Wert -->
        <p>
          rangeVal: <span>{{ rangeVal }}</span>
        </p>
      </section>
    </div>
  </div>
</template>

<script>
import ChildComponentInput from "./components/ChildComponentInput.vue";
import imgFish from "@/assets/img_fish.svg";
import imgTiger from "@/assets/img_tiger.svg";
import SlotComponent from "./components/SlotComponent.vue";
import DataSlotComponent from "./components/DataSlotComponent.vue";

export default {
  components: { ChildComponentInput, SlotComponent, DataSlotComponent },
  name: "App",
  data() {
    return {
      counter: 0,
      exists: false,
      word: "apple",
      text: "I likeburrito , Thai beef salad, pho soup and tagine.", // text: 'I like burrito, pizza, Thai beef salad, pho soup and tagine.' Startwert
      imgs: ["pizza", "cake", "fish", "rice"],
      indexNbr: 0,
      inputValue: null,
      parentBananeValue: "",
      bgColor: false,
      msg: [],
      clickTimes: 0,
      scrollTimes: 0,
      imgFishActive: true,
      imgUrl: imgFish,
      pVisible: false,
      divVisible: false,
      rangeVal: 40,
    };
  },
  watch: {
    rangeVal: {
      handler(val) {
        // Wenn Wert zwischen 20 und 70 liegt
        if (val > 20 && val < 70) {
          // kleiner als 40 → automatisch auf 20 setzen
          if (val < 40) {
            this.rangeVal = 20;
          }
          // größer/gleich 40 → automatisch auf 70 setzen
          else {
            this.rangeVal = 70;
          }
        }
      },
      immediate: true,
    },
  },
  methods: {
    reset() {
      this.counter = 0;
    },
    nextImg() {
      this.indexNbr++;
    },
    changeImg() {
      this.imgFishActive = !this.imgFishActive;
      this.imgUrl = this.imgFishActive ? imgFish : imgTiger;
    },
    onImgClick(event) {
      if (event.shiftKey) {
        this.changeImg();
      }
    },
    onAfterEnter() {
      this.divVisible = true;
    },
  },
  computed: {
    btnText() {
      return this.exists ? "Ausblenden" : "Anzeigen";
    },
    imgActive() {
      return this.imgs[this.indexNbr % this.imgs.length];
    },
  },
};
</script>
<style>
.v-enter-from {
  opacity: 0;
}
.v-enter-to {
  opacity: 1;
  translate: 0 0;
}
.v-leave-from {
  opacity: 1;
  translate: 0 0;
}
.v-leave-to {
  opacity: 0;
}

p {
  background-color: lightgreen;
  display: inline-block;
  padding: 10px 20px;
  transition: all 0.5s;
  margin: 20px 0;
}

.v-enter-active {
  animation: swirlAdded 0.7s;
}

.v-leave-active {
  animation: swirlAdded 0.7s reverse;
}

@keyframes swirlAdded {
  from {
    opacity: 0;
    rotate: 0;
    scale: 0.1;
  }
  to {
    opacity: 1;
    rotate: 360deg;
    scale: 1;
  }
}
img {
  width: 100px;
  margin: 20px;
}
img:hover {
  cursor: pointer;
}
#app {
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem;
  font-family: sans-serif;
}

h1 {
  text-align: center;
  margin-bottom: 2rem;
}

.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 1.5rem;
}

.card {
  background: #fff;
  border-radius: 12px;
  padding: 1rem 1.5rem;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  transition: transform 0.2s ease;
}
.card:hover {
  transform: translateY(-4px);
}

.card h2 {
  margin-bottom: 0.8rem;
  font-size: 1.2rem;
  border-bottom: 1px solid #eee;
  padding-bottom: 0.4rem;
}

button {
  margin: 0.3rem;
  padding: 0.4rem 0.8rem;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  background: #4caf50;
  color: white;
}

img {
  width: 100%;
  max-width: 200px;
  border-radius: 8px;
}

.green {
  background-color: #e0f7e9;
  border-left: 4px solid #4caf50;
  padding: 0.5rem 0.8rem;
  display: block;
  border-radius: 6px;
  margin: 0.5rem 0;
}

.yalClass {
  background-color: rgb(255, 255, 136);
}
#parent {
  width: 90%;
  background-color: lightpink;
}
#parent > div {
  cursor: pointer;
  background-color: lightgreen;
}

.card p {
  background: none; /* Standard-p ohne grünen Hintergrund */
  margin: 0.5rem 0;
  padding: 0;
}

.scroll {
  margin: 10px 0;
  padding: 10px;
  border: dashed black 1px;
  width: 200px;
  height: 50px;
  overflow: scroll;
  background-color: lightcoral;
}

span {
  padding: 3px;
  font-weight: bold;
  font-family: "Courier New", Courier, monospace;
  background-color: lightgreen;
}
</style>
