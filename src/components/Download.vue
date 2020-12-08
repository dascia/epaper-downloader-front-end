<template>
  <div>
    <a :href="downloadLink">
      <input type="button" value="download" class="download-button" />
    </a>
  </div>
</template>

<script lang="ts">
import { ref } from 'vue';
export default {
  name: 'download',
  props: {
    downloadLink: { type: String, default: '' },
  },

  setup() {
    return {};
  },
};
</script>

<style scoped>
.download-button {
  cursor: pointer;
  background: #ffbc0e;
  border: none;
  width: 116px;
  padding: 10px 0px 10px 0px;
  /* height: 30px; */
  font-family: 'PT Sans';
  font-size: 1em;
  color: white;
  font-weight: 600;
  text-shadow: 1px 1px 2px #c5930f;
}

.download-button:focus {
  outline: none;
}
</style>
