<template>
  <teleport to="body">
    <!--截图区域-->
    <canvas
      id="screenshortContainer"
      :width="screenShortWidth"
      :height="screenShortHeight"
      ref="screenShortController"
    ></canvas>
    <!--工具栏-->
    <div
      id="toolPanel"
      v-show="toolStatus"
      :style="{ left: toolLeft + 'px', top: toolTop + 'px' }"
      ref="toolController"
    >
      <div class="item-panel square"></div>
      <div class="item-panel round"></div>
      <div class="item-panel right-top"></div>
      <div class="item-panel brush"></div>
      <div class="item-panel text"></div>
      <div class="item-panel save"></div>
      <div class="item-panel close"></div>
      <div class="item-panel confirm"></div>
    </div>
  </teleport>
</template>

<script lang="ts">
import initData from "@/module/screen-short/main-entrance/InitData";
import eventMonitoring from "@/module/screen-short/main-entrance/EventMonitoring";
import { SetupContext } from "@vue/runtime-core";

export default {
  name: "screen-short",
  props: {},
  setup(props: Record<string, any>, context: SetupContext<any>) {
    const data = new initData();
    const screenShortWidth = data.getScreenShortWidth();
    const screenShortHeight = data.getScreenShortHeight();
    const screenShortController = data.getScreenShortController();
    const toolController = data.getToolController();
    const toolStatus = data.getToolStatus();
    const toolLeft = data.getToolLeft();
    const toolTop = data.getToolTop();
    new eventMonitoring(props, context as SetupContext<any>);
    return {
      screenShortWidth,
      screenShortHeight,
      screenShortController,
      toolController,
      toolStatus,
      toolLeft,
      toolTop
    };
  }
};
</script>

<style
  scoped
  lang="scss"
  src="../assets/scss/teleport/screen-short.scss"
></style>
