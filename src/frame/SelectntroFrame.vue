
<script setup>
    import utils from '@/scripts/utils'
    import { ref, onMounted } from 'vue'
    
    const siteConfig = ref(null);
    const readyStatus = ref(false);
    const applicationStore = utils.useApplicationStore();

    onMounted(async () => {
        await utils.axiostool.sendHttpGet(utils.apiConfig.selectntro).then((data) => {
            siteConfig.value = data;
            readyStatus.value = true;
        }).catch(async (error) => {
            throw new Error(error);
        });
    });
</script>

<template>
    <div class="selectntro-frame" :class="applicationStore.isDeviceMobile && 'frame-mobile'">
        <div class="selectntro-box">
            <h1 class="frame-title">为何选择</h1>
            <p class="frame-desc">无需因陌生而胆怯，我眼里都是灰烬~</p>

            <div class="selectntro-data" v-if="readyStatus">
                <div class="selectntro-item" v-for="(item,index) in siteConfig" :key="index">
                    {{ item.title }}
                </div>
            </div>
        </div>
    </div>
</template>

<style>
    @import url("./assets/SelectntroFrame.css");
</style>