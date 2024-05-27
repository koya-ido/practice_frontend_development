<template>
  <h1>{{ headerTitle }}</h1>
  <button @click="onClick(0)">ボタンA</button>
  <button @click="onClick(1)">ボタンB</button>
  <p>{{ viewResult }}</p>
</template>
<script setup lang="ts">
  interface lotteryResult {
    num: number;
    result: boolean;
  }

  const headerTitle = ref<string>("Hello World");
  let viewResult = ref<string>("");
  
  const onClick = (num: number) => {
    lottery(num);
  }

  const lottery = async (num: number) => {
    const {data: response} = await useFetch<lotteryResult>(`http://localhost:8080/lottery/${num}`);
    if (response.value) {
      viewResult.value = response.value.result ? "あたり" : "はずれ";
    }
  }
  
</script>
