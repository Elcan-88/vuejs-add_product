<template>
    <div class="progress">
      <div class="progress-bar bg-info" role="progressbar" :style="{width: progress + '%'}" aria-valuenow="50" aria-valuemin="0" aria-valuemax="100">
        {{ count }}/10
      </div>
    </div>
</template>

<script>
import { eventBus } from "../main.js";

export default {
  data() {
    return {
      count: 0,
      progress: 0
    }
  },
  created() {
    eventBus.$on("progressBarUpdate", (productListCount) => {
      this.count=productListCount;
      this.progress=productListCount*10;
    });
  }
}
</script>