<template>
  <div class="building">
    <div
        class="elevator"
        :style="currentMove"
    >
      <the-elevator
        :elevator="+this.currentFloor + 1"
      />
    </div>
    <div
        class="floor"
        v-for="(item, index) in floors"
        :key="index"
    >
      <button
        @click="moveTo(item.id)"
      ># {{item.title}}</button>
      <p></p>
    </div>
  </div>
</template>

<script>
import TheElevator from "@/components/TheElevator";
export default {
  components: {TheElevator},
  data(){
    return {
      currentFloor: 0,
      floors:[
        {
          id: 0,
          title: '1 - этаж'
        },
        {
          id: 1,
          title: '2 - этаж'
        },
        {
          id: 2,
          title: '3 - этаж'
        },
        {
          id: 3,
          title: '4 - этаж'
        },
        {
          id: 4,
          title: '5 - этаж'
        }
      ],
      duration: 1000
    }
  },
  computed:{
    currentMove(){
      return {
        top: `${this.currentFloor * 100}px`,
        transition: `top ${this.duration / 1000}s`
      }
    }
  },
  methods:{
    moveTo(floor){
      this.currentFloor = floor
      setTimeout(() => {
        this.currentFloor = floor
      }, this.duration)
      localStorage.currentFloor = this.currentFloor
    }
  },
  mounted() {
    if (localStorage.currentFloor){
      this.currentFloor = localStorage.currentFloor
    }
  }
}
</script>

<style lang="scss">

.building {
  position: relative;
  margin: 0 auto;
  button, p {
    margin-left: 120px;
  }
  button {
    margin-top: 40px;
    width: 100px;
    height: 20px;
    border: 1px solid #1ff;
  }
  .floor {
    width: 100%;
    height: 100px;
    border-bottom: 1px solid #faaf45;
  }
  .elevator {
    top: 0;
    position: absolute;
    width: 100px;
    height: 100px;
    background-color: #f35;
    &_number {
      margin-left: -70px;
      margin-top: 20px;
    }
  }
}

/* Reset and base styles  */
* {
  padding: 0px;
  margin: 0px;
  border: none;
}

*,
*::before,
*::after {
  box-sizing: border-box;
}

/* Links */

a,
a:link,
a:visited {
  text-decoration: none;
}

a:hover {
  text-decoration: none;
}

/* Common */

aside,
nav,
footer,
header,
section,
main {
  display: block;
}

h1,
h2,
h3,
h4,
h5,
h6,
p {
  font-size: inherit;
  font-weight: inherit;
}

ul,
ul li {
  list-style: none;
}

img {
  vertical-align: top;
}

img,
svg {
  max-width: 100%;
  height: auto;
}

address {
  font-style: normal;
}

/* Form */
input,
textarea,
button,
select {
  font-family: inherit;
  font-size: inherit;
  color: inherit;
  background-color: transparent;
}

input::-ms-clear {
  display: none;
}

button,
input[type="submit"] {
  display: inline-block;
  box-shadow: none;
  background-color: transparent;
  background: none;
  cursor: pointer;
}

input:focus,
input:active,
button:focus,
button:active {
  outline: none;
}

button::-moz-focus-inner {
  padding: 0;
  border: 0;
}

label {
  cursor: pointer;
}

legend {
  display: block;
}
</style>