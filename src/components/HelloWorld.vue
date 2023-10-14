<template>
  <div class="hello">
    <div class="sub">
      {{current.title}} - {{current.artist}} - {{current.src}}
    </div>
    <div class="buttons">
    <button>prev</button>
    <button v-if="!isplaying" @click="play">play</button>
    <button v-else @click="pause">pause</button>
    <button>next</button>
    </div>
    <div class="playlists">
      <h1>the playlist</h1>
      <h3>
        <li v-for="song in songs" :key="song.src" @click="play(song)">
          {{song.title}} - {{song.artist}}
        </li>
      </h3>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data(){
    return{
      current:{},
      index:0,
      isplaying:false,
      songs:[
        {
          title:"arsham",
          artist:"arshami",
          src:require('../assets/Catchy.mp3')
        },
        {
          title:"takhtegaz",
          artist:'bezilei',
          src:require('../assets/takh.mp3')
        }
      ],
      player:new Audio()
    }
  },
  methods:{
    play(song){
      if(typeof song.src !='undefined'){
        this.current = song;
        this.player.src = this.current.src
      }
      this.player.play()
      this.isplaying = true
    },
    pause(){
      this.player.pause()
      this.isplaying =false
    },
    next(){
      this.index ++;
      this.current = this.songs[this.index];
      this.play(this.current)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
