<template>
    <div class="flex justify-between items-center w-[400px] m-auto mb-[40px] mt-[60px] ">
        <input
            type="text"
            v-model="dataModel"
            @input="dataInput"
            placeholder="Add work..."
            class="
                border-[#d9d1d1]
                border-solid
                border-[1px]
                outline-none
                w-[80%]
                px-[10px]
                py-[4px]
                text-[gray]
            "
        />
        <button
            @click="onClickButton"
            :disabled="disabledButton ? true : false"
            class="
                outline-none
                text-[#fff]
                bg-[gray]
                px-[16px]
                py-[5px]
                hover:bg-[#9b9999]
            "
        >
            Add
        </button>
    </div>

    <ListTodoApp
        v-for="todo in todos"
        :key="todo.id"
        :todo="todo"
        @emitCheckTick="emitCheckIdTick"
        @emitCheckClose="emitCheckIdClose"
    />
</template>





<script>
    import { ref } from 'vue'
    import ListTodoApp from './ListTodoApp.vue'
    import { v4 as uuidv4 } from 'uuid'

    export default {
        name: 'TodoApp',
        components: {
            ListTodoApp,
        },
        setup(){
            const todos = ref([{
                    id: uuidv4(),
                    name: 'Quét nhà',
                    completed: false
                },
                {
                    id: uuidv4(),
                    name: 'Rửa bát',
                    completed: false
                },
                {
                    id: uuidv4(),
                    name: 'Nấu cơm',
                    completed: false
                },
            ])

            const disabledButton = ref(true)

            const dataModel = ref('')

            const onClickButton = () => {
                const newItem = {
                    id: uuidv4(),
                    name: dataModel.value,
                    completed: false
                }

                todos.value.push(newItem)

                dataModel.value = ''

                disabledButton.value = true
            }

            const dataInput = () => {
                if (dataModel.value.length > 0){
                    disabledButton.value = false
                } else{
                    disabledButton.value = true
                }
            }


            //emit of ListToDoApp
            const emitCheckIdTick = id => {
                todos.value = todos.value.map(todo => {
                    if(todo.id === id){
                        todo.completed = !todo.completed
                    }
                    
                    return todo
                })
            }

            //emit of ListToDoApp
            const emitCheckIdClose = id => {
                todos.value = todos.value.filter(todo => todo.id !== id)
            }

            return{
                todos,
                dataModel,
                dataInput,
                onClickButton,
                disabledButton,
                emitCheckIdTick,
                emitCheckIdClose
            }
        },
    }
</script>
