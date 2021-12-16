<template>
  <link rel="stylesheet" type="text/css" href="style.css">
  <div id="container" >
    <div id="map" v-on:click="setlocation">
      {{location}}
      <div v-bind:style="{left: this.location.x + 'px', top: this.location.y + 'px',}">
        T
      </div>


  </div>
</div>
  <header>
    <img src="https://houseofsmith.com/wp-content/uploads/2021/06/DSCF1226-scaled.jpg" title="Company" img>
    <h1>Welcome to Burgers King&trade;</h1>
  </header>
  <main>
<section class="Burger">
  <Burger v-for="burger in burgers"
          v-bind:burger="burger"
          v-bind:key="burger.name"
          v-on:orderedBurger="addOrder($event)"/>
    </section>
    <section id="contact">
          <form>
            <p>
    <label for="Full Name">Name</label><br>
    <input type="text" id="fullname" v-model="fullname" required="required" placeholder="Full name">
</p>
<p>
    <label for="E-mil">E-mail</label><br>
    <input type="email" id="email" v-model="email" required="required" placeholder="E-mail address">
</p>
<p>
   <label for="payop">Payment option</label>be>
   <select id="payop" name="pop" v-model="payop">
       <option>Cash</option>
       <option>Trade something</option>
       <option>Bitcoin</option>
       <option>Other</option>
   </select>
</p>

<label for="Gender">Gender</label><br>

 <input type="radio" id="male" v-model="sex"  value="male" name="radAnswer">
 <label for="male">Male</label><br>

 <input type="radio" id="female" v-model="sex" value="female" name="radAnswer">
 <label for="female">Female</label><br>

 <input type="radio" id="other" v-model="sex"  value="other" name="radAnswer">
 <label for="other">Don't wish to disclose</label><br>

          </form>

  <button v-on:click="placeOrder" type="submit" >
  <img src="path/to/your-button-image.png">
  Send
</button>

      </section>
  </main>
  <footer>
    <hr>
    <h3>Burgers King's burgirs &copy;</h3>
  </footer>
</template>

<script>



import Burger from '../components/Burger.vue'
import io from 'socket.io-client'
import menu from 'C:/Users/O5car/OneDrive/Skrivbord/Denna vecka/GSP/1md031-lab-21/src/assets/menu.json'
const socket = io();




/*function MenuItem (burgerName, cal, myURL, glutenboolean, laktoseboolean){
this.name= burgerName;
this.kCal = cal;
this.img = myURL;
this.gluten = glutenboolean;
this.lactose = laktoseboolean;
}


const burger1 = new MenuItem("Fishburger", 300, "https://www.askideas.com/media/09/Funny-Chicken-Burger.jpg", true, false);
const burger2 = new MenuItem("Cheeseburger", 400, "https://www.askideas.com/media/09/Funny-Chicken-Burger.jpg", true, false);
const burger3 = new MenuItem("Chickenburger", 600, "https://www.askideas.com/media/09/Funny-Chicken-Burger.jpg", false, true);

const burgers = [burger1, burger2, burger3];
console.log(burgers);
*/

export default {
  name: 'Home',
  components: {
    Burger
  },
  data: function () {
    return {
    sex:"",
    email:"",
    fullname:"",
    payop:"",
    burgers: menu,
    orderedBurgers:{},
    location: {x:0,y:0},

    }
  },
  methods: {
    getOrderNumber: function () {
      return Math.floor(Math.random()*100000);
    },

    setlocation: function(event){
    var offset = {x: event.currentTarget.getBoundingClientRect().left,
                  y: event.currentTarget.getBoundingClientRect().top};
    this.location = {
      x: event.clientX - 10 - offset.x, y: event.clientY - 10 - offset.y
    }
    },
    addOrder: function (event) {
      console.log(event.amount);
      this.orderedBurgers[event.name] = event.amount;

    },
    placeOrder: function()
    {
      socket.emit("addOrder", { orderId: this.getOrderNumber(),
                                details: { x: this.location.x,
                                           y: this.location.y },
                                orderItems: [this.orderedBurgers],
                                customer :{name: this.fullname, email: this.email, payment: this.payment, gender: this.sex}
                              }
                 );
    }
  }
}
</script>

<style>


body {
    font-family: 'Comforter Brush', cursive;
    font-size: 12pt;
}

.Gluten {
   color: #ff5500;
border: 4px solid #ff5500;
Padding: 20px;
}

#Gluten {
   text-transform: uppercase;
}

.Gluten {
   color: #ff5500;
}

#Gluten {
   text-transform: uppercase;
}

.Lactose {
   color: #66b3ff;
border: 4px solid #66b3ff;

Margin: 100px 0px 0px 0px;
Padding: 20px;
}

#Lactose {
   text-transform: uppercase;
}

button:hover {
   color: blue;
cursor:grabbing;
}

button{
margin: 10px 40px;

}
header>img{
  width: 1500px;
height: 250px;
overflow:hidden;
object-fit:cover;
opacity: 0.4;
object-position: 10% 90%;
}

div>img{
Margin: 0px;
width: 300px;
height: 300px;
}

header>h1{
margin-top: -250px;
position: absolute;
}


header{
    border-bottom: 1px dashed rgb(2, 2, 2);
    height: 200px;
    overflow: hidden;

}
.Burger {


     display: grid;
     grid-gap: 100px;
     grid-template-columns: 30% 30% 30%;
     background-color: rgb(0, 0, 0);
        color: #ff5500;
 }


 #map {
 width: 1920px;
 height: 1078px;
 background: url("/img/polacks.jpg");
 }

#map div{
  position:absolute;

}

 #container {


 height: 300px;
 width: 300px;
 overflow:scroll;
 }

</style>
