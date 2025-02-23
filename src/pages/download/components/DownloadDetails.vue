<script setup>
import { computed } from 'vue';
import { ElTabs, ElTabPane } from 'element-plus';
import DownloadDetailsMain from './DownloadDetailsMain.vue';
import DownloadDetailsAppleSiliconInstruction from './DownloadDetailsAppleSiliconInstruction.vue';
import { useDownloadPageStore } from '../../../stores/download-page.js';

const props = defineProps({
  isaInfo: {
    type: [
      {
        title: String,
        zhLabel: String,
        enLabel: String,
        popoverData: { content: String, placement: String },
        installer: Object,
        livekit: Object
      }
    ],
    required: true
  },
  sources: {
    type: [{ name: String, loc: String, url: String }],
    required: true
  }
});

const downloadPageStore = useDownloadPageStore();
const activeTab = computed({
  get() {
    return props.isaInfo.title === 'arm64'
      ? downloadPageStore.dialogTabArm64
      : downloadPageStore.dialogTab;
  },
  set(value) {
    if (['installer', 'livekit'].includes(value)) {
      downloadPageStore.dialogTab = value;
    }
    downloadPageStore.dialogTabArm64 = value;
  }
});
</script>

<template>
  <el-tabs v-model="activeTab" class="*:px-2 pb-2">
    <el-tab-pane
      :disabled="!isaInfo.installer"
      label="系统安装盘"
      name="installer">
      <DownloadDetailsMain
        :arch="isaInfo.zhLabel"
        :content="isaInfo.popoverData.content"
        :path="isaInfo.installer.path"
        :sha256sum="isaInfo.installer.sha256sum"
        :sources="sources" />
    </el-tab-pane>
    <el-tab-pane
      :disabled="!isaInfo.livekit"
      label="LiveKit 救援启动盘"
      name="livekit">
      <DownloadDetailsMain
        :arch="isaInfo.zhLabel"
        :content="isaInfo.popoverData.content"
        :path="isaInfo.livekit.path"
        :sha256sum="isaInfo.livekit.sha256sum"
        :sources="sources" />
    </el-tab-pane>
    <el-tab-pane
      v-if="isaInfo.title === 'arm64'"
      label="Apple Silicon 安装向导"
      name="apple-silicon-instruction">
      <DownloadDetailsAppleSiliconInstruction />
    </el-tab-pane>
    <el-tab-pane
      v-if="isaInfo.title === 'arm64'"
      label="设备镜像"
      name="apple-silicon-image"
      disabled>
      <!-- TODO -->
    </el-tab-pane>
    <el-tab-pane
      label="Docker"
      name="docker"
      disabled
    />
    <el-tab-pane
      label="虚拟机镜像"
      name="vm"
      disabled
    />
  </el-tabs>
</template>
