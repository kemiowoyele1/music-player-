<template>
  <div id="app">
   <header>
      <h1>My music</h1>

   </header>
   <main>
     <section class="player">
        <h2 class="song-title">
         {{ current.title }} 
         <!-- <br> <span class="title-span"> {{current.artist}} </span> -->
       
        </h2>
        <div class="control">
          <button class="prev" @click="prev">prev</button>
          <button class="play" v-if="!isPlaying" @click="play">play</button>
          <button class="pause" v-else @click="pause">pause</button>
          <button class="next" @click="next">next</button>
        </div>
      </section>
      <section class="playlist">
         <h3>playlist</h3>
         <button v-for="song in songs" :key="song.src" @click="play(song)" class="(song.src == current.src) ? 'song playing': 'song'">
                        {{song.title}} - {{song.artist  }}
         </button>
      </section>
   </main>
  </div>
</template>
<script>  
export default  {
  name: 'app',
   data (){
     return {
      current:{},
      index:0,
      isPlaying: false,
      songs: [
        {
          title:'glory to GOD',
          artist:'hillsongs',
          src: require('./assets/glory-to-GOD.mp3')

        },
        {
           title:'GOD bless the USA',
          artist:'Christy Lee Cook',
          src: require('./assets/GOD-bless-the-USA.mp3')

        },
        {
           title:'hes alive',
          artist:'Dolly Parton',
          src: require('./assets/hes-alive.mp3')

        },
         {
           title:'silver and gold',
          artist:'Dolly Parton',
          src: require('./assets/silver-and-gold.mp3')

        }
      ],
      player: new Audio()
       }
   },
   methods: {
     play (song) {
          if(typeof song.src !="undefined"){
            this.current = song;

            this.player.src = this.current.src;
          }
           this.player.play();
           this.player.addEventListener('ended', function(){
             this.index++;
             if(this.index > this.songs.length - 1){
               this.index = 0;
             }
             this.current = this.songs[this.index];
             this.play(this.current);
           }.bind(this));
           this.isPlaying = true;  
     },
     pause(){
       this.player.pause();
       this.isPlaying = false;
     },
     next(){
          this.index++;
          if(this.index > this.songs.length - 1){
            this.index = 0;
          }
        this.current = this.songs[this.index];
        this.play(this.current);
     },
     prev(){
        this.index--;
          if(this.index < 0){
            this.index = this.songs.length - 1;
          }
        this.current = this.songs[this.index];
        this.play(this.current);

     }
   },
   created() {
     this.current = this.songs[this.index];
     this.player.src = this.current.src;
    //  this.player.play();
   }
}
</script>
<style lang="scss">

*{
  margin:0;
  padding: 0;
  box-sizing: border-box;
}

body{
  width :100vw;
  overflow: h;
  font-family: sans-serif;
  text-align: center;
  background-color: #aaf;
  background: rgb(238,174,202);
background: radial-gradient(circle, rgba(238,174,202,0.5) 0%, rgba(196,112,230,0.5) 100%);
}
header{
  display: flex;
  align-items: counter;
  justify-content: center;
  padding: 15PX;
  font-size: 50px;
   color: white;
   animation: header 3s ease infinite;
   background: rgb(175,34,221);
background: linear-gradient(90deg, rgba(175,34,221,1) 5%, rgba(198,146,186,1) 28%, rgba(146,26,193,1) 49%, rgba(206,148,221,1) 68%, rgba(174,25,223,1) 100%);
}
.playlist button{
  display: block;
  padding: 15px;
  margin: 10px;
  min-width: 60%;
  margin-left: 20%;
  font-size: 20px;
  color: plum;
  font-weight: 800;
  background: rgb(107,25,97);
background: radial-gradient(circle, rgba(107,25,97,1) 0%, rgba(163,40,213,1) 100%);

}
.playlist button .song.playing{
  background: radial-gradient(circle, rgb(83, 11, 45) 0%, rgb(175, 118, 147) 100%);

}
.song-title{
   font-size: 30px;
   color:rgb(55, 27, 58);
   padding: 30px;
    animation: title 15s ease infinite;
    white-space: nowrap;
    text-align: left;
  
 }
// .playlist  button:visited{
//   background: red;
// }
.title-span{
  font-size: 20px;
  text-align: center;
}

.control button{
   padding: 10px;
   font-size: 20px;
   margin:20px 5px;
   background-color: purple;
   color: plum;
   border-radius: 20px;
}
.control .play{
  padding:15px;
  font-size: 25px;
  color: pink;
  background-color: rgb(95, 7, 73);
}
@keyframes title{
  0%{
    margin-left: 0;
  }
  100%{
    margin-left: 90vw;
  }
}
 @keyframes header {
    0%{
       background: rgb(175,34,221);
background: linear-gradient(90deg, rgba(175,34,221,1) 5%, rgba(198,146,186,1) 28%, rgba(146,26,193,1) 49%, rgba(206,148,221,1) 68%, rgba(174,25,223,1) 100%);

    }
    50%{
      background: purple;
    }

 100%{
   background: rgb(222,166,228);
background: linear-gradient(90deg, rgba(222,166,228,1) 5%, rgba(154,48,195,1) 28%, rgba(203,116,218,1) 49%, rgba(139,26,167,1) 68%, rgba(202,142,207,1) 100%);}
 }
 
 </style>
