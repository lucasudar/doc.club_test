<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <div class="container pt-5" id="app" v-cloak>
      <div class="card center">
        <div class="form-control" @keypress.enter="addPerson">
          <input type="text" v-model="firstname" placeholder="Enter Name">
          <input type="text" v-model="surname" placeholder="Enter Surname">
          <input type="number" v-model="age" placeholder="Enter Age">
          <button class="btn"
                  @click="addPerson"
          >Add
          </button>
        </div>
        <table>
          <thead>
          <tr>
            <th v-for="col in columns"
                :key="col">
              {{ col }}
            </th>
          </tr>
          </thead>
          <tbody>
          <tr v-for="(person, index) in persons"
              @click.right.prevent="removePerson(index)"
              :key="person.id">
            <td v-for="col in columns"
                :key="col">
              {{ person[col] }}
            </td>
          </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data: () => ({
    firstname: undefined,
    surname: undefined,
    age: undefined,
    persons: [
      {Name: "Chuck", Surname: "Norris", Age: 56},
      {Name: "Bruce", Surname: "Lee", Age: 80},
      {Name: "Jackie", Surname: "Chan", Age: 50},
      {Name: "Jet", Surname: "Li", Age: 35}]
  }),
  props: {
    msg: String,
  },
  watch: {},
  computed: {
    "columns": function columns() {
      if (this.persons.length === 0) {
        return [];
      }
      return Object.keys(this.persons[0])
    }
  },
  methods: {
    addPerson() {
      let newPerson = {
        Name: this.firstname,
        Surname: this.surname,
        Age: this.age
      }
      if (this.firstname === undefined || this.surname === undefined || this.age === undefined) return
      else this.persons.push(newPerson)
      this.firstname = ""
      this.surname = ""
      this.age = ""
    },
    removePerson(index) {
      this.persons.splice(index, 1)
    }
  }

}
</script>

<style scoped>
ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}

body {
  font-family: Inter, Roboto, Oxygen, Fira Sans, Helvetica Neue, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  font-size: 16px;
  color: #2c3e50;
  background: #2c3e50;
}

.btn {
  color: #42b983;
  position: relative;
  place-content: center;
  place-items: center;
  width: fit-content;
  border-radius: 99px;
  letter-spacing: 0.05em;
  border: 1px solid #42b983;
  text-decoration: none;
  text-transform: uppercase;
  margin: 10px;
  padding: 0.5rem 1.5rem;
  white-space: nowrap;
  font-weight: 700;
  outline: none;
  background: #fff;
  transition: all 0.22s;
}

.btn:hover {
  cursor: pointer;
  opacity: 0.8;
}

.btn:active {
  box-shadow: inset 1px 1px 1px rgba(0, 0, 0, 0.3);
}

.container {
  margin: 0 auto;
  max-width: 1000px;
}

.pt-5 {
  padding-top: 5rem;
}

.form-control {
  position: relative;
  display: flex;
  flex-direction: row;
  justify-content: center;
  padding: 20px;
}

.form-control input {
  margin: 1.5rem;
  outline: none;
  border: 2px solid #ccc;
  display: block;
  width: 100%;
  color: #2c3e50;
  padding: 0.5rem 1.5rem;
  border-radius: 3px;
  font-size: 1rem;
}

.form-control input:active,
.form-control input:focus {
  transition: border 0.22s;
  border: 2px solid #42b983;
}

.card.center {
  display: flex;
  flex-direction: column;
  align-items: center;
}

table {
  border: 1px solid #42b983;
  border-radius: 3px;
  background-color: #fff;
}

th {
  background-color: #42b983;
  color: rgba(255, 255, 255, 0.66);
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

td {
  background-color: #f9f9f9;
}

th,
td {
  min-width: 120px;
  padding: 10px 20px;
}
</style>
