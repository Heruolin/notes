<template>
    <div class="flex">
        <VueDraggable
            ref="el"
            v-model="list"
            :animation="150"
            ghostClass="ghost"
            class="card-container"
            @start="onStart"
            @update="onUpdate"
            @end="onEnd"
        >
            <div v-for="item in list" :key="item.id" class="card-item">
                <el-card shadow="always">
                    <template #header>
                        <div class="card-header">
                            <img
                                src="../assets/Notesimages/test3.jpg"
                                alt="Card image"
                                class="card-image"
                            />
                            <img
                                src="../assets/Notesimages/test3.jpg"
                                alt="Card image"
                                class="card-image"
                            />
                        </div>
                    </template>
                    <div>
                        <h1>{{ title }}</h1>
                    </div>
                    <template #footer>Footer content</template>
                </el-card>
            </div>
        </VueDraggable>
        <div class="flex justify-between">
            <preview-list :list="list" />
        </div>
    </div>
</template>


<script setup lang="ts">
import { ref } from 'vue'
import {
    type DraggableEvent,
    type UseDraggableReturn,
    VueDraggable
} from 'vue-draggable-plus'

interface Notecard {
    id: string;
    title: string;
    img: string[];
    text: string;
}



const list = ref([
    {
        name: 'Joao',
        id: 1
    },
    {
        name: 'Jean',
        id: 2
    },
    {
        name: 'Johanna',
        id: 3
    },
    {
        name: 'Juan',
        id: 4
    }
])

const el = ref<UseDraggableReturn>()

const onStart = (e: DraggableEvent) => {
    console.log('start', e)
}

const onEnd = (e: DraggableEvent) => {
    console.log('onEnd', e)
}

const onUpdate = () => {
    console.log('update')
}
</script>

<style scoped>
/* 容器布局 */
.card-container {
    display: flex;
    flex-wrap: wrap; /* 自动换行 */
    gap: 16px; /* 卡片之间的间距 */
    justify-content: center; /* 水平居中 */
    padding: 16px; /* 容器的内边距 */
}

/* 每张卡片样式 */
.card-item {
    flex: 1 1 calc(25% - 8px); /* 每行 3 个卡片，间距占位 */
    max-width: calc(25% - 18px); /* 防止卡片过宽 */
    box-sizing: border-box;
}

/* 卡片图片样式 */
.card-image {
    width: 100%;
    height: auto;
    border-radius: 4px; /* 图片圆角，可选 */
    margin-bottom: 8px; /* 图片和内容之间的间距 */
}

/* 拖拽时的视觉反馈 */
.ghost {
    opacity: 0.5;
    background: #c8ebfb;
}

/* 卡片标题对齐 */
.card-header {
    text-align: center;
}
</style>