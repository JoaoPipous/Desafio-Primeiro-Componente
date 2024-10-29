<template>
  <div class="container">
    <h1>Cadastro de Filmes e Séries</h1>
    
    <div v-if="message" class="message">{{ message }}</div>
    
    <form @submit.prevent="addItem">
      <div class="input-group">
        <label for="name">Nome:</label>
        <input type="text" v-model="newItem.name" id="name" required />
      </div>
      <div class="input-group">
        <label for="Genero">Gênero:</label>
        <select v-model="newItem.Genero" id="Genero" required>
          <option value="Ação">Ação</option>
          <option value="Comédia">Comédia</option>
          <option value="Terror">Terror</option>
          <option value="Suspense">Suspense</option>
          <option value="Animação">Animação</option>
          <option value="Thriller">Thriller</option>
          <option value="Indie">Indie</option>
        </select>
      </div>
      <div class="input-group">
        <label for="type">Tipo:</label>
        <select v-model="newItem.type" id="type" required>
          <option value="Filme">Filme</option>
          <option value="Série">Série</option>
        </select>
      </div>

      <div class="input-group">
        <label for="rating">Nota:</label>
        <select v-model="newItem.rating" id="rating" required>
          <option v-for="n in 11" :key="n" :value="n-1">{{ n-1 }}</option>
        </select>
      </div>

      <div class="input-group">
        <label for="watchedDate">Data que assistiu:</label>
        <input type="date" v-model="newItem.watchedDate" id="watchedDate" required />
      </div>

      <button type="submit" class="btn-submit">Cadastrar</button>
    </form>

    <div v-if="items.length === 0">
      <p>Não há itens cadastrados.</p>
    </div>
    
    <ul v-else>
      <li v-for="(item, index) in items" :key="index" class="item">
        Nome: {{ item.name }}<br>
        Gênero: {{ item.Genero }}<br>
        Categoria: {{ item.type }}<br>
        Nota: {{ item.rating }}<br>
        Assistido em: {{ new Date(item.watchedDate).toLocaleDateString('pt-BR') }}<br>
        <button @click="deleteItem(index)" class="btn-delete">Deletar</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newItem: {
        name: '',
        type: 'Filme',
        Genero: 'Ação',
        rating: null,
        watchedDate: ''
      },
      items: [],
      message: ''
    };
  },
  methods: {
    addItem() {
      if (this.newItem.name && this.newItem.type && this.newItem.rating !== null && this.newItem.watchedDate) {
        this.items.push({ ...this.newItem });
        this.resetForm();
        this.message = '';
      } else {
        this.message = 'Por favor, preencha todos os campos!';
      }
    },
    deleteItem(index) {
      this.items.splice(index, 1);
    },
    resetForm() {
      this.newItem.name = '';
      this.newItem.type = 'Filme';
      this.newItem.Genero = 'Ação';
      this.newItem.rating = null;
      this.newItem.watchedDate = '';
    }
  }
};
</script>

<style scoped>
html, body {
  height: 1500%;
  margin: 1000;
}

body {
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #2c2c2c; 
}

.container {
  width: 100%;
  max-width: 500px;
  background-color: #3b3b3b;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  text-align: center;
}

h1 {
  margin-bottom: 20px;
  font-size: 24px;
  color: white;
}

.input-group {
  margin-bottom: 15px;
}

label {
  display: block;
  margin-bottom: 5px;
  font-weight: bold;
  color: white;
}

input, select {
  width: 100%;
  padding: 10px;
  margin-bottom: 10px;
  border: 2px solid transparent;
  border-radius: 5px;
  background-color: #e0e0e0;
  outline: none;
  transition: border 0.3s;
}

input:focus, select:focus {
  border: 2px solid;
  border-image-slice: 1;
  border-image-source: linear-gradient(to right, red, orange, yellow, green, blue, indigo, violet);
}

button {
  padding: 10px 20px;
  font-size: 16px;
  color: white;
  background-color: #1f7aec;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s;
}


.btn-submit {
  width: 100%;
  background-color: #28a745; 
}

.btn-submit:hover {
  background-color: #218838;
}

.btn-delete {
  margin-top: 10px;
  background-color: #dc3545;
}

.btn-delete:hover {
  background-color: #c82333;
}


ul {
  list-style-type: none;
  padding: 0;
  margin-top: 20px;
}

li.item {
  background-color: #444;
  padding: 15px;
  margin-bottom: 10px;
  border-radius: 5px;
  border: 2px solid transparent;
  transition: border 0.3s;
}

li.item:hover {
  border-image-slice: 1;
  border-image-source: linear-gradient(to right, red, orange, yellow, green, blue, indigo, violet);
}

.message {
  color: #ff4d4d;
  margin-bottom: 15px;
  font-weight: bold;
}
</style>
