<template>
    <div id="item">
        <ul>
            <span>
                <li v-for="item in lista" :key="item.id"><span>{{ item.text }} </span> <button
                        @click="concluir(item.key)">Concluir</button></li>

            </span>
        </ul>
    </div>
</template>
<script>
export default {
    name: 'Item',
    props: [
        'lista',
        'delete'
    ],
    data() {
        return {

        }
    },
    methods: {
        concluir(key) {
            this.delete(key);
        }
    }
}
</script>
<style scoped>
#item {
    white-space: pre-wrap;
    word-wrap: break-word;
}

ul {
    list-style: none;
    padding: 0;
    margin-top: 20px;
}

ul li {
    padding: 15px 0;
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: space-between;
}

li:not(:first-child) {
    border-top: 1px solid #eee;
}

span {
    color: #0D2636;
}

button {
    cursor: pointer;
    background: #DDD;
    color: #000;
    border: 0;
    padding: 8px 8px;
    outline: none;
    border-radius: 4px;
}
</style>