<template>
  <div id="app">
   <header>
      <h1>{{current.title}} <br>   {{current.artist}}</h1>

   </header>
   <main>
     <section class="player">
     
          <div id="container">
            <div id="d1" class="lo">  </div>
            <div id="d2" class="lo">  </div>
            <div id="d3" class="lo">  </div>
            <div id="d4" class="lo">  </div>
            <div id="d5" class="lo">  </div>
            <div id="d6" class="lo">  </div>
            <div id="d7" class="lo">  </div>
            <div id="d8" class="lo">  </div>
            <div id="d9" class="lo">  </div>
            <div id="d10" class="lo">  </div>
        </div>
             <!-- <h2 class="song-title">
         {{ current.title }} 
          <br> <span class="title-span"> {{current.artist}} </span> 
       
        </h2> -->
        <div class="control">
          <button class="prev" @click="prev">prev</button>
          <button class="play" v-if="!isPlaying" @click="play">play</button>
          <button class="pause" v-else @click="pause">pause</button>
          <button class="next" @click="next">next</button>
        </div>
      </section>
      <section class="playlist">
         <!-- <h3>playlist</h3> -->
        
         <button v-for="song in songs" :key="song.src" @click="play(song)" class="(song.src == current.src) ? 'song playing': 'song'">
                        {{song.title}} <br> {{song.artist  }}
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
           title:'Nigeria My Beloved Country',
          artist:'Funmi Adams',
          src: require('./assets/nigeria.mp3')

        },
        {
           title:'hes alive',
          artist:'Dolly Parton',
          src: require('./assets/hes-alive.mp3')

        },
         {
           title:'Nigeria yi',
          artist:'King Sunny Ade',
          src: require('./assets/gbe.mp3')

        },
         {
           title:'which way Nigeria',
          artist:'Sunny Okosun',
          src: require('./assets/which.mp3')

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
           container.style.display='flex';
     },
     pause(){
       this.player.pause();
       this.isPlaying = false;
          container.style.display='none';
   
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
  
  font-family: sans-serif;
  text-align: center;
 background:url(./assets/paper.jpg);
 background-size: 100% 100%;
 background-repeat: no-repeat;
}
header{
  display: flex;
  align-items: counter;
  justify-content: center;
  padding: 15PX;
  font-size: 20px;
   color: white;
   text-shadow: 1px 1px rgb(10, 54, 16), -1px -1px rgb(10, 54, 16);
   animation: header 6s ease infinite;
  background: rgb(16,209,38);
background: linear-gradient(0deg, rgba(16,209,38,0.9612219887955182) 0%, rgba(240,240,229,1) 48%, rgba(223,221,30,1) 100%);}
.playlist button{
  display: block;
  padding: 7px;
  margin: 10px;
  min-width: 60%;
  margin-left: 20%;
  font-size: 13px;
  color: plum;
  font-weight: 800;
  background-color: rgb(70, 230, 83);
   color: rgb(8, 53, 19);
  border-radius: 20px;
}
.playlist button .song.playing{
 background-color: rgb(46, 230, 55);
   color: rgb(9, 53, 29);
  
}
.song-title{
   font-size: 13px;
   color:rgb(10, 54, 16);
   padding: 30px;
    animation: title 15s ease infinite;
    white-space: nowrap;
    text-align: left;
  
 }
// .playlist  button:visited{
//   background: red;
// }
.title-span{
  font-size: 12px;
  text-align: center;
}

.control button{
   padding: 10px;
   font-size: 16px;
   margin:20px 5px;
   background-color: rgb(57, 214, 104);
   color: rgb(8, 61, 8);
    border-radius: 20px;
}
.control .play{
  padding:10px;
  font-size: 20px;
 background-color: rgba(205,209,16,1);
   color: rgb(47, 58, 47);
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
     background: rgb(16,209,38);
background: linear-gradient(90deg, rgba(16,209,38,0.9612219887955182) 0%, rgba(240,240,229,1) 48%, rgba(223,221,30,1) 100%);  }
    50%{
 background: rgb(205,209,16);
background: linear-gradient(90deg, rgba(205,209,16,0.9612219887955182) 0%, rgba(240,240,229,1) 48%, rgba(30,223,33,1) 100%);
}
 100%{
 background: rgb(244,245,225);
background: linear-gradient(90deg, rgba(244,245,225,0.9612219887955182) 0%, rgba(213,234,132,1) 14%, rgba(20,222,43,1) 38%, rgba(23,222,73,1) 59%, rgba(224,226,138,1) 85%, rgba(205,228,205,1) 100%);
}
 }
#container{
    width: 300px;
    height: 140px;
    margin: 20px auto;
    display: flex;
    flex-direction: row;
    align-items: center;
    display:none;
}

.lo{
    width: 30px;
    height: 20px;
    background-color: deeppink;
    margin: 1px;
    border-radius: 50%;
    animation: lod 2.2s ease-in-out infinite;
}

#d1{
    animation-delay: 0.0s;
}
#d2{
    animation-delay: 0.1s;
    animation-name: mod;
}
#d3{
    animation-delay: 0.2s;
}
#d4{
    animation-delay: 0.3s;
       animation-name: mod;

}
#d5{
    animation-delay: 0.4s;
    
}
#d6{
    animation-delay: 0.5s;
       animation-name: mod;

}
#d7{
    animation-delay: 0.6s;
}
#d8{
    animation-delay: 0.7s;
       animation-name: mod;

}
#d9{
    animation-delay: 0.8s;
}
#d10{
    animation-delay: 0.9s;
       animation-name: mod;

}





@keyframes lod{
    0%, 50%, 100%{
        height: 130px;
     background: rgb(69,232,102);
background: linear-gradient(0deg, rgba(69,232,102,1) 0%, rgba(247,251,251,1) 51%, rgba(221,37,8,1) 100%); }
    25%, 75%{
        height: 20px;
 background: rgb(238,171,246);
background: linear-gradient(0deg, rgba(238,171,246,1) 0%, rgba(247,251,251,1) 51%, rgba(230,128,193,1) 100%); }
}

@keyframes mod{
    0%, 50%, 100%{
        height: 20px;
    background: rgb(171,246,190);
background: linear-gradient(0deg, rgba(171,246,190,1) 0%, rgba(247,251,251,1) 51%, rgba(237,162,176,1) 100%);
    }
    25%, 75%{
        height: 130px;
    background: rgb(32,37,33);
background: linear-gradient(0deg, rgba(32,37,33,1) 0%, rgba(247,251,251,1) 51%, rgba(237,220,166,1) 100%);    }
}
 </style>
