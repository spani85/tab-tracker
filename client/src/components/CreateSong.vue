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
          v-model="song.albumImageUrll"
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

      <v-btn class="cyan" dark @click="create">Create Song</v-btn>
    </v-flex>
  </v-layout>
</template>

<script>
import Panel from '@/components/Panel'
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
    async create () {
      this.error = null
      const areAllFieldsFilledIn = Object
        .keys(this.song)
        .every(key => !!this.song[key])

      if (!areAllFieldsFilledIn) {
        this.error = 'Please fill in all the song fields'
        return
      }

      try {
        await SongsService.post(this.song)
        this.$router.push({
          name: 'songs'
        })
      } catch (err) {
        console.log(err)
      }
    }
  },
  components: {
    Panel
  }
}
</script>

<style scoped></style>