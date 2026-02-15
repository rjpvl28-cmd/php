<template>
{{ title }}
<button
@click="loadTitle"
>Загрузить данные</button>
</template>

<script>
import axios from 'axios';
export default {
data() {
    return {
        title: '',
    }
},
methods: {
    async loadTitle() {
        const result = await axios.get('http://mysql.be/index.php')
        this.title = result.data.title
    }
}
}
</script>