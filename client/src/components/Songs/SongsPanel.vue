<template> 
  <panel title="Songs">

    <v-btn 
      fab 
      medium 
      absolute
      right 
      light 
      middle 
      to="/songs/create"
      class="cyan accent-2" 
      slot="action">
      <v-icon>add</v-icon>
    </v-btn>

    <div v-for="song in songs" :key="song.id" class="song">
      <v-layout>
        <v-flex xs6>
          <div class="song-title">
            {{song.title}}
          </div>
          <div class="song-artist">
            {{song.artist}}
          </div>
          <div class="song-genre">
            {{song.genre}}
          </div>

          <v-btn
            dark
            :to="{name: 'song', params: {songId: song.id}}"
            class="cyan">
            View
          </v-btn>
        </v-flex>

        <v-flex xs6>
          <img class="album-image" :src="song.albumImageUrl" />
          <figcaption>{{song.album}}</figcaption>
        </v-flex>
      </v-layout>
    </div>
  </panel>
</template>

<script>
import SongsService from '@/services/SongsService'
export default {
  data () {
    return {
      songs: null
    }
  },
  watch: {
    '$route.query.search': {
      immediate: true,
      async handler (value) {
        this.songs = (await SongsService.index(value)).data
      }
    }
  }
}
</script>

<style scoped>
.song {
  padding: 20px;
  height: 330px;
  overflow: hidden;
}
.song-title {
  font-size: 30px;
}
.song-artist {
  font-size:24px;
}
.sing-genre {
  font-size: 18px;
}
.album-image {
  width: 100%;
}
</style>