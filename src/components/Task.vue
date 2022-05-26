<template>
    <div id="task">
        <form @submit.prevent="addItem">
            <input type="text" placeholder="Tarefa de hoje" v-model="tarefa" />
            <button type="submit">Adicionar</button>
        </form>
        <ItemVue :lista="tarefas" :delete="deleteTask" />
        <span v-show="tarefas.length > 0">
            Você tem <strong :class="{ pend: pendente }">{{ tarefas.length }}</strong> tarefas pendentes
        </span>
    </div>
</template>

<script>
import ItemVue from './Item.vue';
export default {
    name: 'Task',
    components: {
        ItemVue
    },
    data() {
        return {
            tarefa: '',
            tarefas: [],
            pendente: false
        }
    }, methods: {
        addItem() {
            if (this.tarefa.trim().length == 0) {
                alert("Favor, informar uma tarefa!");
                return;
            } else {
                this.tarefas.push({
                    text: this.tarefa,
                    key: Date.now()
                });
                console.log(this.tarefas);
                this.tarefa = '';
            }
        },
        deleteTask(key) {
            let filtro = this.tarefas.filter((item) => {
                return item.key !== key;
            });
            return this.tarefas = filtro;
        }
    }, watch: {
        tarefas: {
            deep: true,
            handler() {
                localStorage.setItem('tasks', JSON.stringify(this.tarefas));
                this.pendente = this.tarefas.length > 4 ;
            }
        }
    }, created() { //chamando automaticamente
        const json = localStorage.getItem('tasks');
        this.tarefas = JSON.parse(json) || [];
    }
}
</script>

<style scoped>
#task {
    max-width: 700px;
    background: #fff;
    border-radius: 4px;
    padding: 20px;
    margin: 20px auto;
    box-shadow: 0 0 20px rgba(0, 0, 0, 0.3);
}

form {
    margin-top: 30px;
    display: flex;
    flex-direction: row;
}

form button {
    cursor: pointer;
    background: #0F5959;
    border: 0;
    border-radius: 4px;
    margin-left: 10px;
    padding: 0 15px;
    display: flex;
    justify-content: center;
    align-items: center;
    color: #FFF;
}

input {
    flex: 1;
    border: 1px solid #eee;
    padding: 6px 10px;
    border-radius: 4px;
    font-size: 14px;
    outline: none;
}

.pend {
    color: red;
}
</style>