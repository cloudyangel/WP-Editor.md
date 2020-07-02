<template>
  <Card class="image-cell">
    <img v-bind:src="url" />
    <p class="image-cell-file-name image-cell-text">{{ filename }}</p>
    <Divider style="margin: 10px 0;" size="small" dashed />
    <div class="image-cell-datetime-size-group">
      <p class="image-cell-datetime image-cell-text">{{ datetime }}</p>
      <p class="image-cell-width-height-size image-cell-text">
        {{ width }}px * {{ height }}px | {{ fileSizeCalculate(size) }}
      </p>
    </div>
    <div class="image-cell-control-group">
      <div class="image-cell-control-group-left">
        <Tooltip v-bind:content="$t('image_cell.delete_this_image')" placement="bottom">
          <Button style="padding: 0 3px;" icon="md-trash"></Button>
        </Tooltip>
      </div>
      <div class="image-cell-control-group-right">
        <Tooltip v-bind:content="$t('image_cell.copy_image_link')" placement="bottom">
          <Button style="padding: 0 3px;" icon="md-copy"></Button>
        </Tooltip>
        <Tooltip v-bind:content="$t('image_cell.download_image')" placement="bottom">
          <Button style="padding: 0 3px;" icon="md-cloud-download"></Button>
        </Tooltip>
        <Tooltip v-bind:content="$t('image_cell.open_image_in_new_tab')" placement="bottom">
          <Button style="padding: 0 3px;" icon="md-open"></Button>
        </Tooltip>
      </div>
    </div>
  </Card>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";

@Component({
  props: ["filename", "width", "height", "size", "datetime", "url"],
})
export default class ImageCell extends Vue {
//   filename = "屏幕截图-202312321213210010102012312.jpg";
//   width = 320;
//   height = 224;
//   size = 801933;
//   datetime = "2000-01-02 12:13:14";
//   url = "https://i.loli.net/2020/06/26/MVS7BqwImvxLXuk.jpg";
  fileSizeCalculate(sizeByte: number): string {
    // 处理NaN的情况
    if (isNaN(sizeByte)) {
      return "";
    }

    if (sizeByte < 1024) {
      // Byte
      return sizeByte.toString() + "B";
    } else if (sizeByte >= 1024 && sizeByte < 1024 * 1024) {
      // KB
      return (sizeByte / 1024).toFixed(2).toString() + "KB";
    } else {
      // MB
      return (sizeByte / 1024 / 1024).toFixed(2).toString() + "MB";
    }
  }
}
</script>

<style lang="scss">
.image-cell {
  width: 320px;

  & img {
    width: 286px;
    height: 200px;
  }

  & p {
    margin: 4px 10px;
    text-overflow: ellipsis;
    white-space: nowrap;
    overflow: hidden;

    &.image-cell-text {
      text-align: left;
      font-size: 0.92em;
    }

    &.image-cell-file-name {
      font-size: 1em;
    }
  }

  & .image-cell-datetime-size-group {
    display: flex;
    justify-content: space-between;
  }

  & .image-cell-control-group {
    text-align: right;
    margin-top: 10px;
    display: flex;
    justify-content: space-between;

    & button {
      margin: 0 2px;
    }
  }
}
</style>