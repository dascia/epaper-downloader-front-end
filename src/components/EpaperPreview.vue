<template>
    <img class="cover-preview" :src="cover" />
</template>
<script lang="ts">
export default {
    name: 'epaper-preview',
    props: {
        cover: { type: String, value: '' },
    },
    setup() {
        return {};
    },
};
</script>

<style scoped>
.cover-preview {
    object-fit: contain;
    max-height: 100%;
}
</style>
