<template>
  <div id="app">
    <TodoHeader>애플리케이션 이름</TodoHeader>
    <TodoInput v-on:addTodo="addTodo">할 일 입력, 수정</TodoInput>
    <TodoList v-bind:propsdata="todoItems" @removeTodo="removeTodo">할 일 목록 표시 및 특정 할 일 삭제</TodoList>
    <TodoFooter v-on:removeAll="clearAll">할 일 모두 삭제</TodoFooter>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue'
import TodoInput from './components/TodoInput.vue'
import TodoList from './components/TodoList.vue'
import TodoFooter from './components/TodoFooter.vue'

export default {
  data() {
    return {
      todoItems: []
    }
  },
  methods: {
    clearAll() {
      localStorage.clear();
      this.todoItems = [];
    },
		addTodo(todoItem) {
      // 로컬 스토리지에 데이터를 추가하는 로직
			localStorage.setItem(todoItem, todoItem);
			this.todoItems.push(todoItem);
		},
    removeTodo(todoItem, index) {
      localStorage.removeItem(todoItem);
      this.todoItems.splice(index, 1);
    }
  },
  created() {
		if (localStorage.length > 0) {
			for (var i = 0; i < localStorage.length; i++) {
				this.todoItems.push(localStorage.key(i));
			}
		}
  },
  components: {
    'TodoHeader': TodoHeader,
    'TodoInput': TodoInput,
    'TodoList': TodoList,
    'TodoFooter': TodoFooter
  }
}
</script>

<style>
  body {
    text-align: center;
    background-color: #F6F6F8;
  }
  input {
    border-style: groove;
    width: 200px;
  }
  button {
    border-style: groove;
  }
  .shadow {
    box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03)
  }
</style>