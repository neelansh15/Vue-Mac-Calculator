<template>
  <div class="calculator">
      <div class="display">
          <div class="topbar">
              <div class="circle red"></div>
              <div class="circle yellow"></div>
              <div class="circle green"></div>
          </div>
          <div class="text">
            {{ current || '0'}}
          </div>
      </div>
      <div class="btn" @click="clear">AC</div>
      <div class="btn" @click="sign">+ / -</div>
      <div class="btn" @click="percent">%</div>
      <div class="btn operator" @click="divide" :class="opclicked">/</div>
      <div class="btn" @click="append(7)">7</div>
      <div class="btn" @click="append(8)">8</div>
      <div class="btn" @click="append(9)">9</div>
      <div class="btn operator" @click="multiply" :class="opclicked">x</div>
      <div class="btn" @click="append(4)">4</div>
      <div class="btn" @click="append(5)">5</div>
      <div class="btn" @click="append(6)">6</div>
      <div class="btn operator" @click="subtract" :class="opclicked">-</div>
      <div class="btn" @click="append(1)">1</div>
      <div class="btn" @click="append(2)">2</div>
      <div class="btn" @click="append(3)">3</div>
      <div class="btn operator" @click="add" :class="opclicked">+</div>
      <div class="btn zero" @click="append(0)">0</div>
      <div class="btn" @click="dot">.</div>
      <div class="btn operator" @click="equal">=</div>
  </div>
</template>

<script>
export default {
    data(){
        return{
            previous: null,
            current: '',
            operator: null,
            operatorClicked: false
        }
    },
    computed: {
        opclicked(){
            if(this.operatorClicked) return "clicked"
            else return ""
        }
    },
    methods:{
        clear(){
            this.current = ''
            this.previous = null
            this.operatorClicked = false
        },
        sign(){
            this.current = this.current.charAt(0) === '-' ? this.current.slice(1) : '-' + this.current
        },
        percent(){
            this.current = (parseFloat(this.current) / 100).toString()
        },
        append(num){
            if(this.operatorClicked){
                this.current = ''
                this.operatorClicked = false
            }
            this.current += num.toString()
        },
        dot(){
            if(this.current.indexOf('.') === -1){
                this.append('.')
            }
        },
        setPrevious(){
            this.operatorClicked = true
            this.previous = this.current
            // this.current = ''
        },
        divide(){
            this.operator = (a, b) => b / a;
            this.setPrevious()
        },
        multiply(){
            this.operator = (a, b) => a * b;
            this.setPrevious()
        },
        subtract(){
            this.operator = (a, b) => b - a;
            this.setPrevious()
        },
        add(){
            this.operator = (a, b) => a + b;
            this.setPrevious()
        },
        equal(){
            this.current = this.operator(
                parseFloat(this.current), 
                parseFloat(this.previous)
            ).toString()
            this.previous = null
        }
    }
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Open+Sans:wght@300&display=swap');

.calculator{
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
    font-size: 1.5rem;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-auto-rows: minmax(50px, auto);
    width: 300px;
    margin: auto;

    color: #1c1c1c;
}
.display{
    padding: 0.5em 0.5em 0.5em 0.5em;
    font-size: 2.5rem;
    text-align: right;
    grid-column: 1 / 5;
    background-color: #505050;
    color: white;
}
.display .text{
    padding-top: 1.5rem;
    font-family: 'Open Sans';
}
.topbar{
    float: left;
    display: flex;
}
.topbar .circle{
    width: 10px;
    height: 10px;
    border-radius: 10px;
    margin: 0 0.25rem;
}
.topbar .red{
    background-color: #FF605c;
}
.topbar .yellow{
    background-color: #FFBD44;
}
.topbar .green{
    background-color: #00CA4E;
}
.zero{
    grid-column: 1 / 3;
    text-align: left;
    padding-left: 20%;
}
.btn{
    /* background-color: #D4D4D2; */
    background-color: rgb(226, 226, 226);
    border: 1px solid rgba(85, 85, 85, 0.6);
    cursor: pointer;
    
    padding-top: 0.5rem;

    /* Set text not selectable */
    -webkit-user-select: none;
     -khtml-user-select: none;
       -moz-user-select: none;
        -ms-user-select: none;
         -o-user-select: none;
            user-select: none;
}
.operator{
    background-color: #ff9500;
    color: white;
}
.operator.clicked{
    background-color: rgb(255, 193, 77);
}
</style>