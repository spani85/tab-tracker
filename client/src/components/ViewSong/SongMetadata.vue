<template>
  <panel title="Song Metadata">
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
          :to="{name: 'song-edit', params: {songId: song.id}}"
          class="cyan">
          Edit
        </v-btn>

        <v-btn
          dark
          v-if="isUserLoggedIn && !bookmark"
          @click="setAsBookmark"
          class="cyan">
          Set As Bookmark
        </v-btn>

        <v-btn
          dark
          v-if="isUserLoggedIn && bookmark"
          @click="unsetAsBookmark"
          class="cyan">
          Unset Bookmark
        </v-btn>
      </v-flex>

      <v-flex xs6>
        <img class="album-image" :src="song.albumImageUrl" />
        <figcaption>{{song.album}}</figcaption>
      </v-flex>
    </v-layout>
  </panel>
</template>

<script>
import {mapState} from 'vuex'
import BookmarksService from '@/services/BookmarksService'
export default {
  data () {
    return {
      bookmark: null
    }
  },
  props: [
    'song'
  ],
  computed: {
    ...mapState([
      'isUserLoggedIn'
    ])
  },
  async mounted () {
    if (!this.isUserLoggedIn) {
      return
    }

    try {
      this.bookmark = (await BookmarksService.index({
        songId: this.song.id,
        userId: this.$store.state.user.id
      })).data
    } catch (err) {
      console.log(err)
    }
  },
  methods: {
    async setAsBookmark () {
      try {
        this.bookmark = (await BookmarksService.post({
          songId: this.song.id,
          userId: this.$store.state.user.id
        })).data
      } catch (err) {
        console.log(err)
      }
    },
    async unsetAsBookmark () {
      try {
        await BookmarksService.delete(this.bookmark.id)
        this.bookmark = null
      } catch (err) {
        console.log(err)
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