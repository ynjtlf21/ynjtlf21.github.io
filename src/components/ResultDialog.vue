<script setup lang="ts">
import {ElDialog, ElButton} from 'element-plus'
import {useCartStore} from "../stores/cart";
import {computed} from "vue";

const cartStore = useCartStore();
const props = defineProps<{
    modelValue: boolean
}>();
const emit = defineEmits(['update:modelValue']);
const mv = computed({
    get: () => props.modelValue,
    set: (v) => emit('update:modelValue', v)
})
</script>

<template>
    <ElDialog
        v-model="mv"
        title="输出结果"
        width="30%"
    >
        <div class="tag-positive">
            <div class="title">正向标签</div>
            <textarea class="tag-pre">{{ cartStore.positiveToString }}</textarea>
        </div>
        <div class="tag-negative">
            <div class="title">反向标签</div>
            <textarea class="tag-pre">{{ cartStore.negativeToString }}</textarea>
        </div>
        <template #footer>
          <span class="dialog-footer">
            <ElButton @click="mv = false">关闭</ElButton>
          </span>
        </template>
    </ElDialog>
</template>

<style scoped>
.tag-positive, .tag-negative {
    margin-bottom: 1.5rem;
}

.title {
    font-size: 14pt;
    margin-bottom: 1rem;
}

.tag-pre {
    resize: vertical;
    width: 100%;
    font-family: Consolas, "Liberation Mono", Menlo, Courier, monospace
}
</style>