<template>
  <div id="add">
    <form action="">
      <fieldset>
        <legend>Greate New Person</legend>
        <div class="form-group">
          <label>Name:</label>
          <input type="text" v-model="newPerson.name">
        </div>
        <div class="form-group">
          <label>Age:</label>
          <input type="text" v-model="newPerson.age">
        </div>
        <div class="form-group">
          <label>Sex:</label>
          <select v-model="newPerson.sex">
            <option value="Male">Male</option>
            <option value="Female">Female</option>
          </select>
        </div>
        <div class="form-group">
          <label></label>
          <button v-on:click.prevent="createPerson">Create</button>
        </div>
      </fieldset>
    </form>
    <div>
      <label for="choose">查询：</label><input type="text" id="choose" v-model="val" v-on:keyup.enter=query(val)>
      <button id="btn" v-on:click=query(val)>提交</button>
      <button id="delBtn" v-on:click = "clear">清除条件</button>
    </div>
    <div class="table_box">
      <table id="people_box">
        <thead>
        <tr>
          <th>Name</th>
          <th>Age</th>
          <th>Sex</th>
          <th>Delete</th>
        </tr>
        </thead>
        <tbody>
        <tr v-for="(person,index) in people">
          <td>{{person.name}}</td>
          <td>{{person.age}}</td>
          <td>{{person.sex}}</td>
          <td class="text-center">
            <button v-on:click="deletePerson(index)">Delete</button>
          </td>
        </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'add',
    data () {
      return {
        val: '',
        newPerson: {
          name: '',
          age: '0',
          sex: 'Male'
        },
        people: [
          {
            name: 'Jack',
            age: '30',
            sex: 'Male'
          },
          {
            name: 'Bill',
            age: '18',
            sex: 'Male'
          },
          {
            name: 'Mary',
            age: '21',
            sex: 'Female'
          }
        ],
        clone: []
      }
    },
    methods: {
      createPerson: function () {
        this.people.push(this.newPerson)
        // 添加完newPerson对象后，重置newPerson对象
        this.newPerson = {
          name: '',
          age: 0,
          sex: 'Male'
        }
      },
      deletePerson: function (index) {
        this.people.splice(index, 1)
      },
      query: function () {
        var data = this.val
        var arr = this.people
        this.clone = arr
        for (var i = 0, arr2 = []; i < arr.length; i++) {
          if ((data === arr[i].name) || (data === arr[i].age) || (data === arr[i].sex)) {
            arr2.push(arr[i])
            this.people = arr2
          }
        }
      },
      clear: function () {
        this.val = ''
        this.people = this.clone
      }
    }
  }
</script>

<style>
  #add {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
  .table_box{
    border:1px solid #333;
    height:500px;
    width:640px;
    overflow: auto;
  }
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box
  }

  html {
    font-size: 12px;
    font-family: Ubuntu, simHei, sans-serif;
    font-weight: 400
  }

  body {
    font-size: 1rem
  }

  table,
  td,
  th {
    border-collapse: collapse;
    border-spacing: 0
  }

  table {
    width: 100%
  }

  td,
  th {
    border: 1px solid #bcbcbc;
    padding: 5px 10px
  }

  th {
    background: #42b983;
    font-size: 1.2rem;
    font-weight: 400;
    color: #fff;
    cursor: pointer
  }

  tr:nth-of-type(odd) {
    background: #fff
  }

  tr:nth-of-type(even) {
    background: #eee
  }

  fieldset {
    border: 1px solid #BCBCBC;
    padding: 15px;
  }

  input {
    outline: none
  }

  input[type=text] {
    border: 1px solid #ccc;
    padding: .5rem .3rem;
  }

  input[type=text]:focus {
    border-color: #42b983;
  }

  button {
    outline: none;
    padding: 5px 8px;
    color: #fff;
    border: 1px solid #BCBCBC;
    border-radius: 3px;
    background-color: #009A61;
    cursor: pointer;
  }
  button:hover{
    opacity: 0.8;
  }

  #app {
    margin: 0 auto;
    max-width: 640px
  }

  .form-group {
    margin: 10px;
  }

  .form-group > label {
    display: inline-block;
    width: 10rem;
    text-align: right;
  }

  .form-group > input,
  .form-group > select {
    display: inline-block;
    height: 2.5rem;
    line-height: 2.5rem;
  }

  .text-center{
    text-align: center;
  }

  .pagination {
    display: inline-block;
    padding-left: 0;
    margin: 21px 0;
    border-radius: 3px;
  }

  .pagination > li {
    display: inline;
  }

  .pagination > li > a {
    position: relative;
    float: left;
    padding: 6px 12px;
    line-height: 1.5;
    text-decoration: none;
    color: #009a61;
    background-color: #fff;
    border: 1px solid #ddd;
    margin-left: -1px;
    list-style: none;
  }

  .pagination > li > a:hover {
    background-color: #eee;
  }

  .pagination .active {
    color: #fff;
    background-color: #009a61;
    border-left: none;
    border-right: none;
  }

  .pagination .active:hover {
    background: #009a61;
    cursor: default;
  }

  .pagination > li:first-child > a .p {
    border-bottom-left-radius: 3px;
    border-top-left-radius: 3px;
  }

  .pagination > li:last-child > a {
    border-bottom-right-radius: 3px;
    border-top-right-radius: 3px;
  }
</style>
