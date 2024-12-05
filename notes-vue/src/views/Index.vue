<template>
  <div class="common-layout">
    <el-container>
      <!-- 头部 -->
      <el-header>
        <div>
          <el-radio-group v-model="isCollapse" style="margin-bottom: 20px">
            <el-button
              @click="toggleCollapse"
              style="display: flex; align-items: center; margin-left: -7px;"
              size="large"
              circle 
            >
              <el-icon v-if="isCollapse" size="large"><Expand /></el-icon>
              <el-icon v-else size="large"><Fold /></el-icon>
            </el-button>
          </el-radio-group>
        </div>  
        
      </el-header>
    </el-container>
    <el-container>
      <!-- 侧边栏 -->
      <el-aside style="width: 200px; min-height: 100vh;">
        <el-menu
          :default-active="$route.path"
          class="el-menu-vertical-demo"
          :collapse="isCollapse"
          @open="handleOpen"
          @close="handleClose"
          style="min-height: 100vh;"
        >
          <!-- 便签 -->
          <el-menu-item index="/">
              <el-icon><House /></el-icon>
              <span>便签</span>
          </el-menu-item>
          <!-- 标签 -->
          <el-sub-menu>
            <template #title>
              <el-icon><CollectionTag /></el-icon>
              <span>标签</span>
            </template>
            <el-menu-item-group>
              <el-menu-item 
              v-for="(item,index) in menuItems"
              :key = "item.index"
              :index="item.index"
              @click="handleItemClick(item)"
              >
                {{ item.label }}
              </el-menu-item>
            </el-menu-item-group>
          </el-sub-menu>
          <!-- 标签修改 -->
          <el-menu-item index="3">
              <el-icon><EditPen /></el-icon>
              <span>标签修改</span>
          </el-menu-item>
          <!-- 笔记本 -->
          <el-menu-item index="4">
            <el-icon><Notebook /></el-icon>
            <template #title>笔记本</template>
          </el-menu-item>
          <!-- 归档 -->
          <el-menu-item index="5">
            <el-icon><Folder /></el-icon>
            <template #title>归档</template>
          </el-menu-item>
          <!-- 垃圾桶 -->
          <el-menu-item index="6">
            <el-icon><Delete /></el-icon>
            <template #title>垃圾桶</template>
          </el-menu-item>
        </el-menu>
      </el-aside>
    <!-- 主体 -->
      <el-main>
        <NotesShow />
      </el-main>

    </el-container>
  </div>
</template>

<script lang="ts" setup>

import { ref } from 'vue'
import {
  Notebook,
  CollectionTag,
  EditPen,
  House,
  Folder,
  Delete,
  Expand,
  Fold
} from '@element-plus/icons-vue'
import NotesShow from '@/components/NotesShow.vue';

// 折叠状态
const isCollapse = ref(true);

// 切换折叠状态
const toggleCollapse = () => {
  isCollapse.value = !isCollapse.value;
};

// 动态菜单数据
const menuItems = ref([
  { index: '2-1', label: '标签1', action: () => alert('标签1被点击') },
  { index: '2-2', label: '标签2', action: () => alert('标签2被点击') },
  { index: '2-3', label: '标签3', action: () => alert('标签3被点击') },
]);

//动态添加标签
menuItems.value.push({
  index: `2-${menuItems.value.length + 1}`,
  label: `标签${menuItems.value.length + 1}`,
  action: () => alert(`动态标签${menuItems.value.length}被点击`),
});

// 处理点击事件
const handleItemClick = (item) => {
  if (item.action) {
    item.action(); // 调用数据中定义的 action 函数
  } else {
    console.log(`${item.label} 被点击，但未定义 action`);
  }
};

const handleOpen = (key: string, keyPath: string[]) => {
  console.log(key, keyPath)
}
const handleClose = (key: string, keyPath: string[]) => {
  console.log(key, keyPath)
}
</script>