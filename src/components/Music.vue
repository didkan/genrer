<template>
  <div class="music">
    <div class="video">
      <youtube @ready="ready" :key="currentVideo.id" v-if="currentVideo" :video-id="currentVideo.id" :player-vars="{start: 0, autoplay: 0}"></youtube>
    </div>
    <div class="result">
      <div>
        <span class="corrects">{{ corrects }}</span>&nbsp;&nbsp;
        <span class="wrongs">{{ wrongs }}</span>
      </div>
      <div>{{ currentVideo && currentVideo.title }}</div>
      <button @click="shuffle()" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded-full">Shuffle</button>
      <div v-if="currentChoice && correctChoice" style="color: green">RÄTT!</div>
      <div v-if="currentChoice && !correctChoice" style="color: red">FEL!</div>
    </div>
    <div class="options">
      <button v-for="(choice, index) in choices" :key="index" @click="guess(choice)" class="bg-transparent hover:bg-blue-500 text-blue-700 font-semibold hover:text-white py-2 px-4 border border-blue-500 hover:border-transparent rounded">
        {{ choice }}
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Music',
  data () {
    return {
      corrects: 0,
      wrongs: 0,
      currentVideo: null,
      currentChoice: null,
      videos: [
        {title: 'Konstmusik orkester', id: '1lHOYvIhLxo'},
        {title: 'Opera', id: 'hAoe7QdZ3ao'},
        {title: 'Körmusik', id: 'eHl8r2g4MXI'},
        {title: 'Folkmusik', id: 'wVx5RJojwnA'},
        {title: 'Kulning', id: 'L7sZ4kx7kQc'},
        {title: 'Irländsk folkmusik', id: 'L5JyVFfBsIg'},
        {title: 'Irländsk folkmusik', id: 'h_IlrRJRXcM'},
        {title: 'Kulning', id: 'KKImmIQ4omQ'},
        {title: 'Blues', id: 'MpRIYi721WE'},
        {title: 'Jazz', id: 'kmfeKUNDDYs'},
        {title: 'Jazz', id: 'qkthxBsIeGQ'},
        {title: 'Rock', id: 'gj0Rz-uP4Mk'},
        {title: 'Rock', id: 'F5fsqYctXgM'},
        {title: 'Pop', id: 'm2uTFF_3MaA'},
        {title: 'Pop', id: 'NEjkftp7J7I'},
        {title: 'Pop', id: 'poXvMBhjSWk'},
        {title: 'Pop', id: 'Sj_9CiNkkn4'},
        {title: 'Gospel', id: '1yUK0S_cEXY'},
        {title: 'Soul', id: 'Q8Tiz6INF7I'},
        {title: 'Country', id: 'JnX2BoZE9w4'},
        {title: 'Country', id: '97svDuqFctI'},
        {title: 'Hårdrock', id: 'eu5lv2Umn3M'},
        {title: 'Punk', id: 'a3UC7dWBDvg'},
        {title: 'Reggae', id: 'S5FCdx7Dn0o'},
        {title: 'Reggae', id: 'vdB-8eLEW8g'},
        {title: 'HipHop', id: 'u31FO_4d9TY'},
        {title: 'Dansbandsmusik', id: 'acf2mw6r8To'},
        {title: 'Dansbandsmusik', id: 'IGz61jY9zIU'},
        {title: 'Schlager', id: 'bSlxoRzrBMs'},
        {title: 'House', id: '1y6smkh6c-0'}
      ]
    }
  },
  mounted() {
    this.shuffle()
  },
  computed: {
    choices () {
      return this.videos.map(video => video.title).filter((v, i, a) => a.indexOf(v) === i)
    },
    correctChoice () {
      return this.currentChoice === this.currentVideo?.title
    }
  },
  methods: {
    ready (event) {
      this.player = event.target
      console.log('ready')
      this.player.playVideo();
    },
    shuffle () {
      const randomIndex = Math.floor(Math.random() * this.videos.length)
      this.currentChoice = null
      this.currentVideo = this.videos[randomIndex]
    },
    play() {
      console.log(this.player)
      this.player.playVideo();
    },
    guess (choice) {
      this.currentChoice = choice
      if (this.correctChoice) {
        this.corrects++
        this.shuffle()
      }
      else{
        this.wrongs++
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

.video {
  width: 1%;
  float: left;
  margin-left: -1000px;
  opacity: 0;
}

.options {
  width: 79%;
  float: left;
  height: 50vh;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  flex: 0 0 30%;
}
.options button {
  display:block;
  width: 20%;
  padding: 10px;
  text-align: center;
  margin: 10px;
  font-size: 1.2em;
}

.result {
  width: 20%;
  float:left;
}
.result div {
  font-size: 40px;
  font-weight: bold;
}
.corrects {
  color: #22C55E;
}
.wrongs {
  color: #EF4444;
}
</style>
