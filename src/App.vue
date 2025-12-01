<script>
import properties from './components/properties.js'
import Landscape from './components/landscape.vue'

export default {
  name: 'App',
  components: { Landscape },
  data() {
    return {
      properties,
      showAvailableOnly: false,
      searchQuery: '',
      sortAsc: true,
    }
  },
  computed: {
    filteredProperties() {
      return this.properties.filter((p) => {
        const matchesSearch =
          p.title.toLowerCase().includes(this.searchQuery.toLowerCase()) ||
          p.location.toLowerCase().includes(this.searchQuery.toLowerCase());
        return matchesSearch && (this.showAvailableOnly ? p.available : true);
      });
    },
    sortedAndFilteredProperties() {
      return [...this.filteredProperties].sort((a, b) => {
        
        const aNum = parseInt(a.price.replace(/[^0-9]/g, '')) || 0;
        const bNum = parseInt(b.price.replace(/[^0-9]/g, '')) || 0;
        return this.sortAsc ? aNum - bNum : bNum - aNum;
      });
    },
  },
  methods: {
    toggleSort() {
      this.sortAsc = !this.sortAsc;
    },
  },
}
</script>
<template>
   <img alt="" class="logo" src="https://thumbs.dreamstime.com/b/houses-sun-waves-vector-design-39164223.jpg" />
  <div class="title">
    <h1>Jacob & Sons Estate Brokers.</h1>
  </div>
  <div>
    <div class="filters">
      <button @click="showAvailableOnly = false" :class="{ active: !showAvailableOnly }">
        All Properties
      </button>
      <button @click="showAvailableOnly = true" :class="{ active: showAvailableOnly }">
        Available Only
      </button>
    </div>

    <div class="search-sort">
      <input type="text" v-model="searchQuery" placeholder="Search by title or location..." />
      <button @click="toggleSort">
        Sort: {{ sortAsc ? 'Low → High' : 'High → Low' }}
      </button>
    </div>

  
    <Landscape :properties="sortedAndFilteredProperties" />
  </div>
</template>

<style scoped>
 .title {
  top: 0;
  left: 0;
  right: 0;
  display: flex;
  justify-content: center;
  padding: 10px 0;
}


.logo {
  padding-top: 10px;
  display: block;
  height:300px;
  width:400px;
  margin: 0 auto 2rem;
  font-family:fantasy;

}

.filters {
  margin-top: 15px;
  display: flex;
  gap: 12px;
  justify-content: center;
  flex-wrap: wrap;
}

.filters button {
  padding: 8px 18px;
  border-radius: 20px;
  border: none;
  cursor: pointer;
  font-weight: 600;
  background: white;
  color: #34495e;
  transition: 0.25s ease;
}

.filters button.active {
  background: #1b263b;
  color: white;
}

.filters button:hover {
  transform: translateY(-2px);
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}


body {
  width: 100%;
  font-family: 'Poppins', sans-serif;
  background: #f5f7fa;
}

.app {
  max-width: 1300px;
  margin: auto;
  padding: 20px;
}

.header {
  background: linear-gradient(90deg, #4b79a1, #283e51);
  padding: 20px;
  border-radius: 12px;
  color: white;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
  margin-bottom: 35px;
  position: top;
}

.nav-bar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
}



.title {
  font-size: 1.5rem;
  text-align: center;
  flex: 1;
  margin: 10px 0;
  font-weight: 600;
  position: top;
  color: teal;
}

.wishlist {
  font-weight: bold;
  font-size: 1.2rem;
}


.property-grid {
  display: grid;
  gap: 25px;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
}

@media (max-width: 768px) {
  .nav-bar {
    flex-direction: column;
    text-align: center;
  }



  .property-grid {
    grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  }
}


@media (max-width: 480px) {
  .title {
    font-size: 1.2rem;
  }

}

.search-sort {
  margin-top: 15px;
  display: flex;
  gap: 12px;
  justify-content: center;
  flex-wrap: wrap;
}

.search-sort input {
  padding: 8px 12px;
  border-radius: 20px;
  border: none;
  width: 250px;
  max-width: 100%;
}

.search-sort button {
  padding: 8px 18px;
  border-radius: 20px;
  border: none;
  background: #34495e;
  color: white;
  cursor: pointer;
  font-weight: 600;
}

</style>