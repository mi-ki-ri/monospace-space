<template>
  <div
    id="app"
    class="lg:container mx-auto min-h-screen flex justify-between items-stretch"
  >
    <div class="flex w-1/2 min-h-screen">
      <textarea
        class="w-full m-2 p-2 font-mono"
        v-model="textareaVal"
        id="t-area"
        @keydown.tab.prevent=""
      ></textarea>
    </div>
    <div class="flex w-1/2 min-h-screen" id="p-area" @click="dl">
      <pre class="w-full m-2 p-2 font-mono">{{ textareaVal }}</pre>
    </div>
  </div>
</template>

<script>
import html2canvas from "html2canvas";

export default {
  name: "App",
  data() {
    return {
      textareaVal: "",
    };
  },
  methods: {
    dl() {
      const tArea = document.getElementById("p-area");

      html2canvas(tArea)
        .then((newCanvas) => {
          newCanvas.classList.add("w-full");
          newCanvas.classList.add("p-2");
          newCanvas.classList.add("m-2");
          let link = document.createElement("a");

          link.href = newCanvas.toDataURL("image/png");
          link.download = `monospace${new Date().toLocaleString()}.png`;
          link.click();
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
};
</script>

<style>
div {
  border: 1px solid #ccc;
}
</style>
