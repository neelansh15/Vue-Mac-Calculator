<template>
  <div class="calculator">
      <div class="display">{{ current || '0'}}</div>
      <div class="btn" @click="clear">C</div>
      <div class="btn" @click="sign">+ / -</div>
      <div class="btn" @click="percent">%</div>
      <div class="btn operator">/</div>
      <div class="btn" @click="append(7)">7</div>
      <div class="btn" @click="append(8)">8</div>
      <div class="btn" @click="append(9)">9</div>
      <div class="btn operator">x</div>
      <div class="btn" @click="append(4)">4</div>
      <div class="btn" @click="append(5)">5</div>
      <div class="btn" @click="append(6)">6</div>
      <div class="btn operator">-</div>
      <div class="btn" @click="append(1)">1</div>
      <div class="btn" @click="append(2)">2</div>
      <div class="btn" @click="append(3)">3</div>
      <div class="btn operator">+</div>
      <div class="btn zero" @click="append(0)">0</div>
      <div class="btn" @click="dot">.</div>
      <div class="btn operator">=</div>
  </div>
</template>

<script>
export default {
    data(){
        return{
            current: '153'
        }
    },
    methods:{
        clear(){
            this.current = ''
        },
        sign(){
            this.current = this.current.charAt(0) === '-' ? this.current.slice(1) : '-' + this.current
        },
        percent(){
            this.current = (parseFloat(this.current) / 100).toString()
        },
        append(num){
            this.current += num.toString()
        },
        dot(){
            if(this.current.indexOf('.') === -1){
                this.append('.')
            }
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
}
.operator{
    background-color: orange;
    color: white;
}
</style>