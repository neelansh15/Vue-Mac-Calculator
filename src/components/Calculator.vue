<template>
  <div class="calculator">
      <div class="display">{{ current || '0'}}</div>
      <div class="btn" @click="clear">C</div>
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
            this.operator = (a, b) => a / b;
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
.calculator{
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
    font-size: 2rem;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-auto-rows: minmax(50px, auto);
    width: 40%;
    min-width: 40%;
    max-width: 60%;
    margin: auto;
}
.display{
    padding: 1em 0.5em 0.5em 0.5em;
    font-size: 2.5rem;
    text-align: right;
    grid-column: 1 / 5;
    background-color: #181818;
    color: white;
}
.zero{
    grid-column: 1 / 3;
    text-align: left;
    padding-left: 20%;
}
.btn{
    background-color: #eeeeee;
    border: 1px solid #e2e2e2;
    cursor: pointer;

    /* Set text not selectable */
    -webkit-user-select: none;
     -khtml-user-select: none;
       -moz-user-select: none;
        -ms-user-select: none;
         -o-user-select: none;
            user-select: none;
}
.operator{
    background-color: orange;
    color: white;
}
.operator.clicked{
    background-color: rgb(255, 193, 77);
}
</style>