<template>
    <div class="main-container">
        <div class="preview-container">
            <epaper-preview :cover="cover"></epaper-preview>
        </div>
        <div class="controls-container">
            <edition-selector @edition-selected="requestEPaperInfo"></edition-selector>
            <download class="btn-download" :downloadLink="downloadLink"></download>
        </div>
    </div>
</template>
<script lang="ts">
import { computed, ref, watch } from 'vue';
import EpaperPreview from './EpaperPreview.vue';
import EditionSelector from './EditionSelector.vue';
import Download from './Download.vue';
export default {
    name: 'epaper-downloader',
    components: {
        EpaperPreview,
        EditionSelector,
        Download,
    },
    setup() {
        
        const tempCover = ref<string>('');
        const cover = ref<string>('./assets/not-available.jpg');
        const downloadLink = ref<string>('');

        // Watch cover function
        watch(tempCover, (newVal: string, preVal: string) => {
            console.log('cover current value: ', tempCover.value);
            console.log('preval: ', preVal, 'new val', newVal);
            fetch(tempCover.value).then(
                _ => {
                    console.log('cover exists.');
                    cover.value = newVal;
                },
                _ => {
                    console.log('cover not exists.');
                    cover.value = './assets/not-available.jpg';
                }
            );
        });

        // Request the epaper json file containing the cover and download link
        function requestEPaperInfo(editionDate: string): void {
            console.log('Start request');
            const request = `https://elmundo-epaper-api.herokuapp.com/api/v1/epaper?date=${editionDate}`;
            fetch(request)
                .then(
                    r => r.json(),
                    _ => console.log(_)
                )
                .then(epaperJson => {
                    tempCover.value = epaperJson['cover'];
                    downloadLink.value = epaperJson['epaper'];
                });
        }

        return {
            cover,
            tempCover,
            downloadLink,
            requestEPaperInfo,
        };
    },
};
</script>
<style scoped>
.main-container {
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: column;
}

.preview-container {
    width: 100%;
    flex-grow: 1;
    overflow: hidden;
}

.controls-container {
    width: 100%;
    margin-top: auto;
    flex-grow: 0;
}

.btn-download {
    margin-top: 10px;
}
</style>
