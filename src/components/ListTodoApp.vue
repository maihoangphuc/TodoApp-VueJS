<template>
    <div class="flex w-[400px] items-center m-auto mb-[30px] ">
        <div class="flex w-[100%] items-center gap-x-[20px]">
            <input
                :id="todo.id"
                type="checkbox"
                :checked="todo.completed"
                @change="onChangeCheckBox"
                class="
                    form-check-input
                    appearance-none
                    h-[20px]
                    w-[20px]
                    border
                    border-[#d9d1d1]
                    checked:bg-[#7dcf7d]
                    checked:border-[#7dcf7d]
                    cursor-pointer
                "
            />
            <div class="w-[85%]">
                <label
                    :for="todo.id"
                    :class="[
                        'text-[gray] break-all cursor-pointer',
                        todo.completed ? 'line-through' : ''
                    ]"
                >
                    {{ todo.name }}
                </label>
            </div>
        </div>

        <font-awesome-icon
            :icon="['fas', 'close']"
            class="text-[gray] cursor-pointer"
            @click="onClickClose"
        />
    </div>
</template>



<script>
    export default {
        name: 'ListTodoApp',
        props: ['todo'],
        setup(props, contex){
            const onChangeCheckBox = () => {
                contex.emit('emitCheckTick', props.todo.id)
            }

            const onClickClose = () => {
                contex.emit('emitCheckClose', props.todo.id)
            }

            return{
                onChangeCheckBox,
                onClickClose
            }
        }
    }
</script>

