<template>
  <v-layout>
    <v-flex xs4>
      <panel title="Song Metadata">
        <v-text-field
          label="Title"
          required
          :rules="[rules.required]" 
          v-model="song.title"
          ></v-text-field>

          <v-text-field
          label="Artist" 
          v-model="song.artist"
          required
          :rules="[rules.required]" 
          ></v-text-field>

          <v-text-field
          label="Genre" 
          v-model="song.genre"
          required
          :rules="[rules.required]" 
          ></v-text-field>

          <v-text-field
          label="Album" 
          v-model="song.album"
          required
          :rules="[rules.required]" 
          ></v-text-field>

          <v-text-field
          label="Album Image Url" 
          v-model="song.albumImageUrl"
          required
          :rules="[rules.required]" 
          ></v-text-field>

          <v-text-field
          label="YouTube ID" 
          v-model="song.youtubeId"
          required
          :rules="[rules.required]" 
          ></v-text-field>
      </panel>
    </v-flex>

    <v-flex xs8>
      <panel title="Song Structure" class="ml-2">
        <v-text-field
          label="Tab" 
          multi-line
          v-model="song.tab"
          required
          :rules="[rules.required]" 
          ></v-text-field>

        <v-text-field
          label="Lyrics" 
          multi-line
          v-model="song.lyrics"
          required
          :rules="[rules.required]" 
          ></v-text-field>

      </panel>

      <v-alert error value=true v-if="error" v-html="error" class="ml-2"></v-alert>

      <v-btn class="cyan" dark @click="save">Save</v-btn>
    </v-flex>
  </v-layout>
</template>

<script>
import SongsService from '@/services/SongsService'
export default {
  data () {
    return {
      song: {
        title: null,
        artist: null,
        genre: null,
        album: null,
        albumImageUrl: null,
        youtubeId: null,
        lyrics: null,
        tab: null
      },
      rules: {
        required: (value) => !!value || 'Required.'
      },
      error: null
    }
  },
  methods: {
    async save () {
      this.error = null
      const areAllFieldsFilledIn = Object
        .keys(this.song)
        .every(key => !!this.song[key])

      if (!areAllFieldsFilledIn) {
        this.error = 'Please fill in all the song fields'
        return
      }

      const songId = this.$store.state.route.params.songId

      try {
        await SongsService.put(this.song)
        this.$router.push({
          name: 'song',
          params: {
            songId: songId
          }
        })
      } catch (err) {
        console.log(err)
      }
    }
  },
  async mounted () {
    const songId = this.$store.state.route.params.songId
    this.song = (await SongsService.show(songId)).data
  }
}
</script>

<style scoped></style>