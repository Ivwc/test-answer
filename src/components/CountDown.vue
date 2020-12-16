<template>
  <div class="count-down">
    倒数：{{ counting }}
  </div>
</template>

<script>
  export default {
    name: 'count-down',
    data() {
      return {
        needCount: 36000000
      }
    },
    computed: {
      counting: function() {
        // console.log('时',Math.floor(this.needCount/3600000));
        // console.log('分',Math.floor(this.needCount%3600000/60000));
        // console.log('秒',Math.floor(this.needCount%3600000%60000/1000));
        let hour = Math.floor(this.needCount / 3600000);
        let min = Math.floor((this.needCount % 3600000) / 60000);
        let sec = Math.floor(((this.needCount % 3600000) % 60000) / 1000);
        // console.log('computed time ',`${min<10?'0'+min:min}:${sec<10?'0'+sec:sec}`);
        // 把小时加到分里
        // min = hour * 60 + min;
        if (hour <= 0 && min <= 0 && sec <= 0) {
          clearInterval(this.interval);
          this.interval == "";
          return `00:00`;
        } else {
          return `${hour < 10 ? "0" + hour : hour}:${min < 10 ? "0" + min : min}:${sec < 10 ? "0" + sec : sec}`;
        }
      },
    },
    created() {
      this.interval = setInterval(() => {
        this.needCount = this.needCount - 1000;
      }, 1000);
    }
  }
</script>

<style lang="less" scoped>
.count-down {
  background: white;
  margin: 10px 0;
  margin-bottom: 20px;
  padding: 16px;
}
</style>