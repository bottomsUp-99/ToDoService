<script>
export default {
  props: {
    // 현재 필터링 상태를 부모로부터 받음 (all 또는 completed)
    current: {
      type: String,
      default() {
        return "all"; // 기본값은 'all'
      },
    },
  },
  emits: ["update-tab"], // 탭 변경 이벤트를 부모로 전달
  methods: {
    // 탭이 변경될 때 부모 컴포넌트로 이벤트 전달
    updateTab(tab) {
      this.$emit("update-tab", tab);
    },
  },
};
</script>

<template>
  <div class="todo__title">
    <h1 class="todo__text">Todo List</h1>
    <ul class="todo__tab">
      <!-- '전체' 탭 클릭 시, 'all' 상태로 전환 -->
      <li
        :class="{ 'todo__tab--active': current === 'all' }"
        @click="updateTab('all')"
      >
        전체
      </li>
      <!-- '완료' 탭 클릭 시, 'completed' 상태로 전환 -->
      <li
        :class="{ 'todo__tab--active': current === 'completed' }"
        @click="updateTab('completed')"
      >
        완료
      </li>
    </ul>
  </div>
</template>
