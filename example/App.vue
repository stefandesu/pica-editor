<template>
  <div>
    <PicaEditor
      ref="editor"
      :unapi="unapi"
      :dbkey="dbkey"
      :picabase="picabase"
      @change="recordChanged" />  
    <div
      v-if="examples && examples.length"
      style="font-size: smaller; padding-top: 0.2em;">
      Beispiele:
      <ul class="inline">
        <li
          v-for="ex in examples"
          :key="ex">
          <a @click="loadRecord(ex)">{{ ex }}</a>
        </li>
      </ul>
    </div> 
  </div>
</template>

<script>
import PicaEditor from "../src/PicaEditor.vue"

const config = {
  unapi: "https://unapi.k10plus.de/",
  dbkey: "opac-de-627",
  picabase: "https://opac.k10plus.de/",
  avram: "https://format.k10plus.de/avram.pl",
  examples: [ "161165839X", "1673636357", "168675535X" ],
}

export default {
  components: { PicaEditor },
  data() { return {...config} },
  methods: {
    loadRecord(ppn) {
      // Use $nextTick to give dbkey the chance to propagate to PicaEditor
      this.$nextTick(() => {
        this.$refs.editor.loadRecord(ppn)
      })
    },
    recordChanged() {
      console.log("recordChanged")
    },
  },
}
</script>
