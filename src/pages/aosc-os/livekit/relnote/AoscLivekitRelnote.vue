<script setup>
import CategorySecond from '/src/components/CategorySecond.vue';
</script>

<template>
  <div class="pl-[1px]">
    <category-second title="发行注记：2025 年 4 月" />
    <div class="p-6">
      <p>LiveKit 是用于维护安同 OS 和进行故障修复的可移动环境，本次发行包含的新特性与更改如下。 </p><br />
    </div>

    <category-second title="新特性与更改" id="features" />
    <div class="p-6">
      <p>
        除将系统组件更新到 2025 年 4 月的基线外，LiveKit 还包含如下新特性：
      </p><br />
      <div class="px-16 pt-2 pb-4">
        <ul class="list-disc">
          <li>更新 Linux 内核至 6.14.1，支持更多新硬件</li>
          <li>改进下拉菜单操作逻辑，安装可在仅使用键盘的情况下完成</li>
          <li>修复安装时未禁止使用系统预留用户名的问题</li>
          <li>修复系统安装后未正确探测设备上其他操作系统的问题</li>
          <li>修复安装过程中屏幕可能熄灭，导致用户不安的问题</li>
          <li>新增安装程序日志记录功能</li>
          <li>新增多语言启动菜单支持</li>
          <li>新增使用 LEFI 固件的龙芯三号 (MIPS) 3A4000/3B4000 平台安装支持</li>
        </ul>
      </div>
    </div>
  </div>
</template>

<style scoped></style>
./components/Header.vue
