<template>
  <div v-scroll-reveal.reset class="wrap">
    <div class="container">
      <div class="container-1">
        <h1>Add Your Tasks</h1>
        <hr>
        <div class="filters">
          <button class="btn-about" @click="showCompleted = !showCompleted">
            {{ showCompleted ? 'Show all' : 'Hide completed' }}
          </button>
        </div>
        <ul>
          <li v-for="kegiatan in filteredKegiatan" :key="kegiatan.id">
            <div class="kegiatan-info">
              <div class="kegiatan-list">
                <input type="checkbox" v-model="kegiatan.completed">
                <span :class="{ completed: kegiatan.completed }">{{ kegiatan.nama
                }}
                </span>
              </div>
              <button class="btn-about" @click="deleteKegiatan(kegiatan)">Delete</button>
            </div>
          </li>
        </ul>
        <form @submit.prevent="addKegiatan">
          <input type="text" required v-model="newKegiatan" placeholder="Add a task">
          <button class="btn-about" type="submit">Add</button>
        </form>
      </div>
      <p class="creator">Created by <a href="https://www.instagram.com/_mdzakyefendi/" target="_blank">M. Dzaky Efendi</a>
      </p>
    </div>
  </div>
</template>
  
<script>
export default {
  data() {
    return {
      kegiatanList: [],
      newKegiatan: '',
      showCompleted: false,
    };
  },
  methods: {
    addKegiatan() {
      const newId = this.kegiatanList.length + 1;
      this.kegiatanList.push({
        id: newId,
        nama: this.newKegiatan,
        completed: false,
      });
      this.newKegiatan = '';
    },
    deleteKegiatan(kegiatan) {
      const index = this.kegiatanList.indexOf(kegiatan);
      this.kegiatanList.splice(index, 1);
    },
    toggleCompleted(kegiatan) {
      kegiatan.completed = !kegiatan.completed;
    },
  },
  computed: {
    filteredKegiatan() {
      return this.showCompleted
        ? this.kegiatanList.filter((t) => !t.completed)
        : this.kegiatanList
    },
  },
};

</script>
  
<style scoped>
.wrap {
  display: flex;
  align-items: center;
  justify-content: center;
}

.container {
  border: 1px solid rgba(255, 255, 255, .5);
  border-radius: 15px;
  backdrop-filter: blur(5px);
  min-width: 250px;
  max-width: 500px;
}

.container .container-1 {
  margin: 30px;
}

.kegiatan-info {
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 100%;
  margin-bottom: 5px;
  border-radius: 50px;
  transition: 0.2s ease;
  right: 20px;
}

.kegiatan-info:hover {
  background-color: #ACB1D6;
}

.btn-about {
  color: var(--color-text);
  background-color: antiquewhite;
  cursor: pointer;
  transition: border-color 0.25s;
  border-radius: 50px;
  border: 1px solid transparent;
  padding: 0.6em 1.2em;
}

input[type="text"] {
  padding: 10px;
  font-family: Arial, sans-serif;
  font-size: 14px;
  border: 1px solid #ccc;
  border-radius: 50px;
  color: #464545;
  background-color: antiquewhite;
}

input[type="text"]:focus {
  outline: none;
  border-color: #ccc;
}

input[type="text"]:hover {
  background-color: white;
}


input[type="checkbox"]::before {
  content: '\2713';
  font-size: 14px;
  position: absolute;
  top: -3px;
  right: -0.px;
  color: #464444;
  visibility: hidden;
}

input[type="checkbox"]:checked::before {
  visibility: visible;
}

input[type="checkbox"] {
  position: relative;
  appearance: none;
  border-radius: 50%;
  width: 15px;
  height: 15px;
  border: 1px solid #ccc;
  background-color: #E4F9F5;
  margin-bottom: -3px;
  top: -2px;
  margin-left: 10px;
}

input[type="checkbox"]:hover {
  border: 2px solid #ccc;
  transition: 0.5ms;
  cursor: pointer;
}

.completed {
  text-decoration: line-through 2px black;
}

.filters {
  margin-bottom: 10px;
}

ul li {
  list-style-type: none;
}

input {
  margin-right: 10px;
}

.creator {
  font-size: smaller;
  color: #F9F7F7;
}

.creator a {
  transition: all ease .5ms;
}

.creator a:hover {
  font-weight: bold;
}

form input {
  border: none;
  border-radius: 3px;
}

h1 {
  font-size: 3.2em;
  line-height: 1.1;
  color: #F9F7F7;
  margin-bottom: 2px;
  font-weight: bolder;
}
</style>
  
