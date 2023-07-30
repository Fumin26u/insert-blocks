<script setup lang="ts">
import { ref } from 'vue'
const blocks = ref<string[]>(['a', 'b', 'c', 'd', 'e'])

// 指定した方向に要素を移動
const changeOrder = (index: number, direction: number) => {
    // 指定した方向に要素がない場合は終了
    if (index + direction < 0 || blocks.value.length <= index + direction) {
        return
    }

    // 前または後ろの要素と入れ替え
    const arg = blocks.value[index]
    blocks.value[index] = blocks.value[index + direction]
    blocks.value[index + direction] = arg
}
</script>

<template>
    <section class="block-field">
        <div v-for="(block, index) in blocks" :key="index">
            <div class="block">
                <p>{{ block }}</p>
            </div>
            <div class="button-area">
                <button @click="changeOrder(index, -1)">←</button>
                <button @click="changeOrder(index, 1)">→</button>
            </div>
        </div>
    </section>
</template>

<style lang="scss">
.block-field {
    max-width: 1000px;
    display: flex;
    justify-content: space-between;
    box-sizing: border-box;
}

.block {
    border: 4px solid #aaa;
    width: 160px;
    height: 160px;
    > p {
        margin: 0;
        padding: 56px;
        font-size: 32px;
        text-align: center;
    }
}

.button-area {
    width: 100%;
    > button {
        width: 50%;
        display: inline-block;
        vertical-align: middle;
    }
}
</style>
