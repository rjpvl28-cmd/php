<template>
{{ title }}
<button
@click="loadTitle"
>Загрузить данные</button>
<table>
    <tr>
        <td>ID</td>    
        <td>Имя</td>
        <td>Фамилия</td>
        <td>Возраст</td>    
    </tr>
    <tr
        v-for="user in users"
        :key="user.id"
    >
        <td>{{ user.id }}</td>    
        <td>{{ user.firstname}}</td>
        <td>{{ user.secondname }}</td>
        <td>{{ user.age }}</td>    
    </tr>
</table>
<form>
    <input 
        type="text" 
        placeholder="Имя"
        v-model="firstname"
        >
    <input 
        type="text" 
        placeholder="Фамилия"
        v-model="secondname"
        >
    <input 
        type="text" 
        placeholder="Возраст"
        v-model="age"
        >
    <button
        @click.prevent="addUser"
    >Создать пользователя</button>
</form>
</template>

<script>
import axios from 'axios';
export default {
data() {
    return {
        title: '',
        users: [],
        firstname: '',
        secondname: '',
        age: null,
    }
},
methods: {
    async loadTitle() {
        const result = await axios.get('http://mysql.be/index.php')
        this.title = result.data.title
        this.users = result.data.users
    },
    async addUser() {
        await axios.post('http://mysql.be/index.php'), {
            firstname: this.firstname,
            secondname: this.secondname,
            age: this.age
        } 
            
    } 
}
}
</script>

<style>
    table, td {
        border: 1px solid black;
    }
    
    table {
        border-collapse: collapse;
    }

    td {
        padding: 5px 10px;
    }
</style>