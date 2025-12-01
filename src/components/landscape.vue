<script>
export default {
  name: 'Landscape',
  props: {
    properties: {
      type: Array,
      required: true
    }
  },
  methods: {
    toNumber(price) {
      return parseInt(price.replace(/[^0-9]/g, '')) || 0;
    }
  }
}
</script>

<template>
  <div class="container">
    <div class="property" v-for="property in properties" :key="property.id">
      <div class="card_box">
        <img :src="property.img" class="img" />
        <p>{{ property.title }}</p>
        <p>{{ property.location }}</p>
        <p>R {{ toNumber(property.price).toLocaleString() }}</p>
        <p>{{ property.property_type }}</p>
      </div>
    </div>
  </div>
</template>


<style scoped>
.property {
  padding-top: 10px; 
  align-items: center;
  justify-content: center;
  display: grid
}
.container {
  align-items: center;
  justify-content: center;
  height:600px;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  display: grid;
  gap: 20px;
 
}
.img{
  width:400px;
  height:140px;
  object-fit: cover;
  justify-items: center;
}
.card_box {
  width: 400px;
  height: 250px;
  border-radius: 20px;
  background: linear-gradient(170deg, rgba(58, 56, 56, 0.623) 0%, rgb(31, 31, 31) 100%);
  box-shadow: 0 25px 50px rgba(0,0,0,0.55);
  cursor: pointer;
  transition: all .3s;
  position: relative; 
  
}

.card_box:hover {
  transform: scale(0.9);
}

.card_box span {
  position: absolute;
  overflow: hidden;
  width: 150px;
  height: 150px;
  top: -10px;
  left: -10px;
  display: grid;
  align-items: center;
  justify-content: center;
}

.card_box span::before {
  content: 'Premium';
  position: absolute;
  width: 150%;
  height: 40px;
  background-image: linear-gradient(45deg, #ff6547 0%, #ffb144  51%, #ff7053  100%);
  transform: rotate(-45deg) translateY(-20px);
  display: grid;
  align-items: center;
  justify-content: center;
  color: #fff;
  font-weight: 600;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  box-shadow: 0 5px 10px rgba(0,0,0,0.23);
}

.card_box span::after {
  content: '';
  position: absolute;
  width: 10px;
  bottom: 0;
  left: 0;
  height: 10px;
  z-index: -1;
  box-shadow: 140px -140px #cc3f47;
  background-image: linear-gradient(45deg, #FF512F 0%, #F09819  51%, #FF512F  100%);
}
</style>
