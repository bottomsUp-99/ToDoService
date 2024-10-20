<script>
export default {
  props: {
    // 부모로부터 필터링된 todo 항목 배열을 받음
    computedTodo: {
      type: Array,
      default() {
        return [];
      },
    },
  },
  methods: {
    // Todo 항목 삭제 요청 시 부모에게 이벤트 전달
    deleteTodo(id) {
      this.$emit("delete-todo", id);
    },
    // Todo 완료 상태 업데이트 요청 시 부모에게 이벤트 전달
    updateTodo(id) {
      this.$emit("update-todo", id);
    },
  },
};
</script>

<template>
  <div class="todo__list">
    <!-- 필터링된 todo 항목을 반복하여 표시 -->
    <div
      v-for="item in computedTodo"
      :key="item.id"
      class="todo__item"
      :class="{ 'todo__item--completed': item.completed }"
    >
      <!-- 완료 상태를 표시하는 체크박스 -->
      <input
        type="checkbox"
        :id="`chk${item.id.toString()}`"
        :checked="item.completed"
        @click="updateTodo(item.id)" /> <!-- 체크박스 클릭 시 상태 변경 -->
      <label :for="`chk${item.id.toString()}`" class="todo__checkbox-label"></label>
      
      <!-- Todo 항목 텍스트 -->
      <span class="todo__item-text">{{ item.msg }}</span>
      
      <!-- 삭제 버튼 -->
      <span
        class="material-symbols-outlined todo__delete-icon"
        @click="deleteTodo(item.id)"> <!-- 삭제 클릭 시 삭제 이벤트 발생 -->
        delete
      </span>
    </div>

    <!-- Todo 항목이 없을 때 보여줄 메시지 -->
    <div v-if="computedTodo.length === 0" class="todo__item--no">
      <p>할 일이 없습니다.</p>
    </div>
  </div>
</template>
