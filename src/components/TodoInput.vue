<script>
export default {
  data() {
    return {
      inputMsg: "", // 사용자가 입력하는 텍스트를 저장
    };
  },
  emits: ["addTodo"], // 부모에게 새로운 todo 추가 이벤트를 전달
  methods: {
    // 새로운 todo 항목을 추가하는 함수
    addTodo() {
      if(this.inputMsg.trim() === ''){ // 입력값이 없거나 공백일 경우
        return; // 아무 작업도 하지 않음
      } else {
      this.$emit("addTodo", this.inputMsg); // 부모 컴포넌트에 새로운 todo 항목 전달
      this.inputMsg = ""; // 입력 필드 초기화
      }
    },
  },
};
</script>

<template>
  <div class="todo__input">
    <!-- 입력 필드, 사용자의 입력을 v-model로 바인딩 -->
    <input
      v-model="inputMsg"
      type="text"
      class="todo__input-text"
      placeholder="할 일을 입력하세요."
      @keyup.enter="addTodo" /> <!-- 엔터키 누르면 addTodo 실행 -->
    <!-- 등록 버튼 클릭 시 addTodo 함수 실행 -->
    <button class="todo__input-btn" @click="addTodo">등록</button>
  </div>
</template>
