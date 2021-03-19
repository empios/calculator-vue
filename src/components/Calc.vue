<template>
  <div class="hero is-danger is-fullheight">
    <div class="hero-body">
      <div class="container has-text-centered ">
        <div class="tile is-ancestor">
          <div class="tile is-vertical is-12">
            <div class="tile is-parent">
              <article class="tile is-child notification is-warning">
                <div class="column">
                  <div style="background-color: azure">
                    <p>{{this.finalString}}</p>
                    <h5>{{this.sum}}</h5>
                  </div>
                </div>
                <div class="columns">
                  <div class="column">
                      <div class="column">
                        <h3>Choose number</h3>
                      </div>
                      <div class="column">
                        <b-button @click="handleClick(1)" class="is-large is-success">1</b-button>
                        <b-button @click="handleClick(2)" class="is-large is-success">2</b-button>
                        <b-button @click="handleClick(3)" class="is-large is-success">3</b-button>
                      </div>
                      <div class="column">
                          <b-button @click="handleClick(4)" class="is-large is-success">4</b-button>
                          <b-button @click="handleClick(5)" class="is-large is-success">5</b-button>
                          <b-button @click="handleClick(6)" class="is-large is-success">6</b-button>
                      </div>
                      <div class="column">
                        <b-button @click="handleClick(7)" class="is-large is-success">7</b-button>
                        <b-button @click="handleClick(8)" class="is-large is-success">8</b-button>
                        <b-button @click="handleClick(9)" class="is-large is-success">9</b-button>
                      </div>
                      <div class="column">
                        <b-button @click="handleClick(0)" class="is-large is-success" style="width: 50%">0</b-button>
                      </div>
                  </div>
                  <div class="column">
                    <div class="column">
                      <h3>Choose operation</h3>
                    </div>
                    <div class="column">
                      <b-button @click="handleOperation('+')" class="is-large is-success" style="width: 50%">Add</b-button>
                    </div>
                    <div class="column">
                      <b-button @click="handleOperation('*')" class="is-large is-success" style="width: 50%">Multiply</b-button>
                    </div>
                    <div class="column">
                      <b-button @click="handleOperation('-')" class="is-large is-success" style="width: 50%">Subtract</b-button>
                    </div>
                    <div class="column">
                      <b-button @click="handleOperation('/')" class="is-large is-success" style="width: 50%">Divide</b-button>
                    </div>
                  </div>
                </div>
                <div class="column">
                  <b-button @click="handleSum" class="is-large is-success" style="width: 50%">=</b-button>
                </div>
              </article>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Calc',
  data() {
    return{
      sum: 0,
      finalString: "",
      finalArr: []
    }
  },
  methods:{
    handleClick: function(number){
      this.finalArr.push(number)
    },
    handleOperation: function (operation){
      this.finalArr.push(operation)
    },
    handleSum: function () {
      let sum = 0;
      let arr = [];
      let tempString = "";
      this.finalArr.map((item, index) => {
        if (typeof item === 'number'){
          if(index === this.finalArr.length-1){
            tempString += item.toString();
            arr.push(tempString);
          }
          tempString += item.toString();
        }
        else {
          if(typeof item === 'string'){
            arr.push(tempString);
            arr.push(item)
            tempString = "";
          }
        }
      })
      arr.map((item,index) => {
        if(item === "+"){
          if(sum === 0) {
            sum = Number(arr[index - 1]) + Number(arr[index + 1])
          }
          else {
            sum = sum + Number(arr[index + 1])
          }
        }
        if(item === "-"){
          if(sum === 0) {
            sum = Number(arr[index - 1]) - Number(arr[index + 1])
          }
          else {
            sum = sum - Number(arr[index + 1])
          }
        }
        if(item === "*"){
          if(sum === 0) {
            sum = Number(arr[index - 1]) * Number(arr[index + 1])
          }
          else {
            sum = sum * Number(arr[index + 1])
          }
        }
        if(item === "/"){
          if(sum === 0) {
            sum = Number(arr[index - 1]) / Number(arr[index + 1])
          }
          else {
            sum = sum / Number(arr[index + 1])
          }
        }
      })
      this.sum = sum;
      this.finalString = ""
      this.finalArr = [];
    }
  },
  watch: {
    finalArr: function () {
      this.finalString = this.finalArr.join("");
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
