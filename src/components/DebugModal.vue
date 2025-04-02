<template>
<ModalComponent :show="show" @close="emit('close')">
  <div class="title is-5 mb-4">
    Debug
  </div>
  <div>
    {{mystring}}
  </div>

    <div class="field has-text-right">
      <div class="control">
        <button class="button mr-2" @click="emit('close')">Close</button>
      </div>
    </div></ModalComponent>
</template>

<script setup lang="ts">

import ModalComponent from "@/components/ModalComponent.vue";
import {watch, ref} from "vue";

const mystring = ref("");

const props = defineProps({
  show: {
    type: Boolean,
    required: true,
  },
});

watch(
  () => props.show,
  (show) => show && getDebugData(),
);

const emit = defineEmits(['close']);


async function getDebugData(){
  let saved = await globalThis.ActiveWorkspace?.provider.getState();
  if (saved == undefined) {
    saved = "";
  }
  console.log(saved);
  mystring.value = saved;
  return saved.toString()
}

</script>

<style scoped lang="scss"/>
