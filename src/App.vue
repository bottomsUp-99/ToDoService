<script>
import TodoHeader from "@/components/TodoHeader.vue";
import TodoList from "@/components/TodoList.vue";
import TodoInput from "@/components/TodoInput.vue";

export default {
  components: {
    // 하위 컴포넌트 등록
    TodoHeader,
    TodoList,
    TodoInput,
  },
  data() {
    return {
      todo: [], // Todo 리스트를 저장하는 배열
      current: "all", // 현재 선택된 필터 상태 (all 또는 completed)
    };
  },
  computed: {
    // 현재 필터링된 todo 항목들을 계산하는 함수
    computedTodo() {
      if (this.current === "all") {
        return this.todo; // 전체 항목 반환
      } else {
        return this.todo.filter((v) => v.completed); // 완료된 항목만 반환
      }
    },
  },
  methods: {
    // 새로운 todo 항목 추가
    addTodo(inputMsg) {
      const item = {
        id: Math.random(), // 고유한 아이디 생성
        msg: inputMsg, // 사용자가 입력한 텍스트
        completed: false, // 기본값으로 미완료 상태
      };
      this.todo.push(item); // todo 리스트에 추가
    },
    // 탭 변경 시 현재 필터 상태 업데이트
    updateTab(tab) {
      this.current = tab;
    },
    // 특정 todo 항목을 삭제하는 함수
    deleteTodo(id) {
      this.todo = this.todo.filter((v) => v.id !== id); // 선택된 id와 다른 항목들만 남김
    },
    // 특정 todo 항목의 완료 상태를 반전시키는 함수
    updateTodo(id) {
      this.todo = this.todo.map((v) =>
        v.id === id ? { ...v, completed: !v.completed } : v
      );
    },
  },
};
</script>

<template>
  <div class="todo">
    <!-- 헤더 컴포넌트, 필터링 상태를 관리 -->
    <TodoHeader :current="current" @update-tab="updateTab" />

    <!-- Todo 리스트 컴포넌트, 필터링된 todo 항목을 표시 -->
    <TodoList
      :computed-todo="computedTodo"
      @delete-todo="deleteTodo"
      @update-todo="updateTodo"
    />

    <!-- Todo 입력 컴포넌트, 새로운 todo 항목을 추가 -->
    <TodoInput @add-todo="addTodo" />
  </div>
</template>
