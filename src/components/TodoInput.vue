<script>
export default {
  data() {
    return {
      inputMsg: "", // 데이터 정의
    };
  },
  emits: ["addTodo"],
  methods: {
    addTodo() {
      if(this.inputMsg.trim() === ''){//inputMsg의 앞뒤 공백을 제거한 후 빈 문자열인지 확인
        return;//만약 입력값이 빈 문자열이거나 공백일 경우, return을 통해 함수 종료. 이때 이벤트도 발생하지 않고 입력 필드도 초기화 X
      } else {
      this.$emit("addTodo", this.inputMsg); // 부모 컴포넌트 이벤트 호출
      this.inputMsg = ""; // 입력 데이터 초기화
      }
    },
  },
};
</script>
<template>
  <div class="todo__input">
    <input
      v-model="inputMsg"
      type="text"
      class="todo__input-text"
      placeholder="할 일을 입력하세요."
      @keyup.enter="addTodo" />
    <button class="todo__input-btn" @click="addTodo">등록</button>
  </div>
</template>