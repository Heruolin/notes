<template>
  <el-button plain @click="centerDialogVisible = true">
    Click to open the Dialog
  </el-button>

  <el-dialog
    v-model="centerDialogVisible"
    :title="title"
    width="650px"
    align-center
    :show-close="false"
  >
    <template #header>
      <!-- 修改标题 -->
      <el-input v-model="title" placeholder="请输入标题"></el-input>
    </template>

    <!-- 图片区域 -->
    <div class="image-gallery">
      <div
        v-for="(image, index) in images"
        :key="index"
        class="image-container"
      >
        <el-image
          :src="image"
          alt="test image"
          class="image"
          :preview-src-list="images"
          :initial-index="index"
        />
        <el-button
          circle
          type="danger"
          size="small"
          icon="Delete"
          @click="deleteImage(index)"
          class="delete-btn"
        />
      </div>
    </div>

    <!-- 便签内容 -->
    <div>
      <el-input
        v-model="textarea"
        style="width: 619px;margin-top: 5px;margin-bottom: 8px;"
        :autosize="{ minRows: 6, maxRows: 20 }"
        type="textarea"
        placeholder="请输入内容"
      />
    </div>

    <!-- 标签 -->
    <div>
      <el-tag
        v-for="tag in tags"
        :key="tag.name"
        closable
        type="primary"
        effect="plain"
        :disable-transitions="false"
        @close="handleClose(tag)"
        round
        style="margin-bottom: -5px;"
      >
        {{ tag.name }}
      </el-tag>
    </div>

    <template #footer>
      <!-- 底部按钮 -->
      <div style="text-align: left;">

        <el-button circle title="添加图片" icon="Picture" @click="AddImg"/>

        <el-button circle title="背景颜色" icon="Orange" @click="BackgroundColor"/>

        <el-button circle title="添加标签" icon="CollectionTag" @click="AddTag"/>

        <el-button circle title="归档" icon="FolderAdd" @click="Archive"/>

        <el-button circle title="删除便签" icon="Failed" @click="Failed" />
        
      </div>
      <div>
        <el-button @click="centerDialogVisible = false">关闭</el-button>
      </div>
    </template>
  </el-dialog>
</template>

<script lang="ts" setup>
import { ref } from "vue";

const centerDialogVisible = ref(false);

const title = ref("当前标题");
const textarea = ref("初始数据");
// 图片组
const images = ref([
  "src/assets/Notesimages/test3.jpg",
]);

//图片删除事件
const deleteImage = index => {
  images.value.splice(index, 1);
};


//图片添加按钮
const AddImg = () => {
  console.log("图片添加事件")
}

//背景色选择按钮
const BackgroundColor = () => {
  console.log("背景颜色事件")
}

//标签添加按钮
const AddTag = () => {
  console.log("添加标签")
}

const Archive = () => {
  centerDialogVisible.value = false
  console.log("归档事件")
}
//便签删除按钮
const Failed = () => {
  centerDialogVisible.value = false
  console.log("便签删除事件")
}

//标签事件
interface TagsItem {
  name: string;
}

const tags = ref<TagsItem[]>([
  { name: "Tag 1" },
  { name: "Tag 2" },
  { name: "Tag 3" },
  { name: "Tag 4" },
  { name: "Tag 5" }
]);

const handleClose = (tag: TagsItem) => {
  tags.value = tags.value.filter(item => item.name !== tag.name);
};
</script>

<style scoped>
/* 图片区域 */
.image-gallery {
  display: flex;
  flex-wrap: wrap; /* 换行支持 */
  justify-content: center; /* 水平居中 */
  align-items: center; /* 垂直居中 */
  gap: 10px; /* 图片间距 */
  padding: 10px;
}

/* 每张图片容器 */
.image-container {
  flex-shrink: 0; /* 图片不缩小 */
  max-width: 619px; /* 限制图片最大宽度 */
  position: relative;
  display: flex;
  justify-content: center; /* 图片居中 */
  align-items: center; /* 图片居中 */
}

/* 图片样式 */
.image {
  width: auto;
  max-width: 100%; /* 图片宽度限制为容器的宽度 */
  max-height: 350px; /* 图片最高限制 */
  border-radius: 4px; /* 圆角样式 */
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2); /* 图片阴影 */
}

/* 隐藏按钮 */
.delete-btn {
  position: absolute;
  bottom: 10px;
  right: 10px;
  display: none;
  z-index: 10;
  transition: opacity 0.3s ease-in-out;
}

/* 鼠标悬停时显示按钮 */
.image-container:hover .delete-btn {
  display: inline-flex;
}
</style>
