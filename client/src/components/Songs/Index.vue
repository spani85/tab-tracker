<template> 
  <v-layout>
    <v-flex xs6>
      <songs-bookmarks />
      <recently-viewed-songs class="mt-2" />
    </v-flex>
    <v-flex xs6 class="ml-2">
      <songs-search-panel />
      <songs-panel class="mt-2" />
    </v-flex>
  </v-layout>
</template>

<script>
import SongsPanel from './SongsPanel'
import SongsBookmarks from './SongsBookmarks'
import SongsSearchPanel from './SongsSearchPanel'
import RecentlyViewedSongs from './RecentlyViewedSongs'
export default {
  components: {
    SongsPanel,
    SongsBookmarks,
    SongsSearchPanel,
    RecentlyViewedSongs
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