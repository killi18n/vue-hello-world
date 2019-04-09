<template>
  <TodoItem/>
</template>

<script lang="ts">
import Vue from 'vue';
import axios from 'axios';
import TodoItem from './todos/TodoItem.vue';
import { Component } from 'vue-property-decorator';

interface TodoType {
    uesrId: number;
    id: number;
    title: string;
    completed: boolean;
}

@Component({
    components: {
        TodoItem,
    },
})
export default class JsonPlaceHolder extends Vue {
    private todos: TodoType[] = [];

    private mounted() {
        this.fetchAPI();
    }

    private async fetchAPI(): Promise<void> {
        try {
            const response = await axios.get(
                'https://jsonplaceholder.typicode.com/todos/1'
            );
            if (response.data) {
                this.todos.concat(response.data);
            }
        } catch (e) {
            throw new Error(e);
        }
    }
}
// export default Vue.extend({
//     props: [],
//     data() {
//         return {
//             todos: [],
//         };
//     },
//     methods: {
//         fetchAPI() {
//             axios
//                 .get('https://jsonplaceholder.typicode.com/todos/1')
//                 .then((response: any) => {
//                     const data = response.data;
//                     this.todos.concat(data);
//                 })
//                 .catch((error: any) => {
//                     // console.log(e);
//                     throw new Error(error);
//                 });
//         },
//     },
//     mounted() {
//         this.fetchAPI();
//     }
// });
</script>
