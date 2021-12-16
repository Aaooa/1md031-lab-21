<template>
<div style="display: inline-block;">
  <h2> {{burger.name}}</h2>
  <img v-bind:src= "burger.img" >

    {{amountOrdered}}
    <button v-on:click="decrease" type="decrease">
  -
</button>

<button v-on:click="addBurger" type="addBurger">
  +
</button>
</div>
</template>

<script>
export default {
  name: 'Burger',
  props: {
    burger: Object
  },
  data: function () {
  return {
    amountOrdered: 0,
  }

},
  methods: {
   decrease: function (){
     if(this.amountOrdered<1) {
       null
     }
     else{
      this.amountOrdered --
    }
  },
   addBurger: function () {
      this.amountOrdered ++
      this.$emit('orderedBurger', {name: this.burger.name,
      amount: this.amountOrdered});
   }
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.Burger {
     display: grid;
     grid-gap: 100px;
     grid-template-columns: 30% 30% 30%;
     background-color: rgb(0, 0, 0);

 }
</style>
