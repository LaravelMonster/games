<template>
  <div class="hello">
  <div>
  <input type="checkbox" v-model="parameters.sensitive" :checked="parameters.sensitive"> Case sensitive
  <input type="checkbox" v-model="parameters.hidethis" :checked="parameters.hidethis"> Add custom texts
  </div>
  <div>
    <div v-if="text == ''" class="stats">
    <table>
      <caption>Stats for your typing practice</caption>
      <thead>
        <tr>
          <th>Key</th>
          <th>Value</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>Total Words</td>
          <td>{{stats.wordCount}}</td>
        </tr>
        <tr>
          <td>Total Time Taken</td>
          <td>{{totalTimeTaken}}</td>
        </tr>
        <tr>
          <td>Total Delete Key Pressed</td>
          <td>{{stats.deleteTimes}}</td>
        </tr>
        <tr>
          <td>Total Words per Minute</td>
          <td>{{wordsPerSecond}}</td>
        </tr>
      </tbody>
    </table>
    <div>
        <button @click="restart">Start Again </button>
      </div>
    </div>
  </div>
  <div>
  </div>
        <div>
          <textarea v-model="customText" class="custom" @keyup.prevent="updateText" v-if="parameters.hidethis" @keyup.enter="parameters.hidethis = !parameters.hidethis"></textarea>
        </div>
        <textarea class="texted" v-model='joinedText' :disabled="true"></textarea>
        <textarea class="input" v-model="input" :value='input' @keyup.delete="deleter" @keyup.space="alerter" :disabled="parameters.hidethis"></textarea>
  </div>
</template>

<script>
export default {
  name: 'hello',
  computed: {
    joinedText: function(){
      if(this.text == ''){
        this.stats.time.end = new Date()
      }
      return this.text.join(' ')
    },
    totalTimeTaken: function(){
      if(this.stats.time.end && this.stats.time.start)
        return (this.stats.time.end - this.stats.time.start) / 1000;
      return 'unavailable'
    },
    wordsPerSecond: function(){
      var totalTimeTaken = this.totalTimeTaken;
      if(totalTimeTaken){
          return Math.round((this.stats.wordCount / totalTimeTaken) * 60);
      }
      return 'unavailable'
    }

  },
  mounted: function(){
    this.updateText()
  },
  methods: {
    alerter: function(){
      this.stats.time.start = this.stats.time.start == '' ? new Date():this.stats.time.start
      this.parameters.hidethis = false
      if(this.equal()){
        this.text = _.drop(this.text)
        this.input = _.reject(_.drop(this.input.split(' ')),' ').join(' ')
      }
    },
    updateText: function(){
    this.text = this.customText.split(' ')
    this.stats.wordCount = this.text.length
    this.stats.time.start = ''
    },
    restart: function(){
      window.location.reload()
    },
    deleter: function(){
        if(this.input != '')
        this.stats.deleteTimes++
    },
    equal: function(){
      var input = this.input.split(' ')[0];
      var text = this.text[0]
      return  this.parameters.sensitive ? input == text : input.toLowerCase() == text.toLowerCase()
    }
  },
  data () {
    return {
      customText: "I will join this as soon as possible.",
      text: [],
      input:'',
      jsonText:[],
      parameters: {
        sensitive:true,
        hidethis: false,
      },
      stats: {
        deleteTimes:0,
        wordCount: 0,
        time:{
          start:0,
          end:0
        }
      }
    }
  }
}
</script>

<style scoped>
  .texted{
    height: 200px;
    width: 35%;
    position: absolute;
    left: 10%;
    border-width: 10px;
    border-color: #5d6b49;
    resize: none;
  }
  .input{
        height: 200px;
    width: 35%;
    position: absolute;
    right: 10%;
    border-width: 10px;
    border-color: #71756b;
    resize: none;
  }
  .custom{
    height: 200px;
    width: 400px;
    right: 15%;
    border-width: 10px;
    border-color: #5e7b34;
    resize: none;
  }
.stats{
        border: 1px solid green;
        border-radius: 10px;
            width: 100%;
            max-width: 500px;
            margin-left: 32%;
      }
.stats thead tr th{
  border-bottom: solid 2px blueviolet ridge;
  border-bottom-style: dashed;
}
.stats table{
  width: 100%;
}
.stats table tbody tr td:first-child{
  border-right: 1px solid black;
  border-right-style: dashed; 
}
</style>
