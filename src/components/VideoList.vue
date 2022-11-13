<template>
  <div class="main">
    <el-row>
      <el-col style="margin-bottom: 10px" v-for="(video) in videos" :key="video.id">
        <el-card :body-style="{padding: '10px'}">
          <img v-bind:src="video.snippet.thumbnails.standardThumbnail.url" alt="">
          <div style="text-align: left;">
            <h3>{{video.snippet.title}}</h3>
          </div>
        </el-card>
      </el-col>
    </el-row>
  </div>
</template>

<script>

export default {
  components: {},
  data() {
    return {
      videos: []
    }
  },
  methods: {
    async fetchVideos() {
      return fetch('http://localhost:8080/videos?channelId=UCBLqkkSpOi6a95Lf4BsTh7Q')
          .then(function (response) {
            return response.json();
          }).then(function (data) {
            return data.items;
          });
    }
  },
  async created() {
    this.videos = await this.fetchVideos();
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.main {
  margin-left: auto;
  margin-right: auto;
  width: 30%;
  padding: 0;
}
img {
  float: left;
  margin-right: 5%;
  margin-bottom: 10px;
  width: 240px;
}
</style>
