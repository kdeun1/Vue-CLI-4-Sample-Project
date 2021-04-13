<template>
  <div>
    <h1>Sample Page</h1>
    <p>For a test sample</p>
    <h3>ON/OFF</h3>
    state : {{ flagText }}
    <button
      @click="changeFlag"
    >
      Change Flag
    </button>
    <h3>Input Text</h3>
    <div>
      ID :
      <input
        type="text"
        v-model="id"
      />
      Name :
      <input
        type="text"
        v-model="name"
      />
      <button
        @click="saveInfo"
      >
        Save
      </button>
    </div>
    <div
      v-for="list in formList"
      :key="list"
    >
      ID : {{ list.id }} | Name : {{ list.name }}
    </div>
  </div>
</template>

<script>
import { ref, reactive, toRefs, onMounted } from 'vue';

export default {
  name: 'Sample',
  components: {
  },
  setup() {
    const flagText = ref('ON');
    const changeFlag = () => {
      if (flagText.value === 'ON') flagText.value = 'OFF';
      else flagText.value = 'ON';
    }

    const formInfo = reactive({
      id: '',
      name: '',
    })
    const formList = ref([]);
    const saveInfo = () => {
      formList.value.push({
        id: formInfo.id,
        name: formInfo.name,
      })
    }

    onMounted(() => {
      console.log('onMounted Hook!');
    });

    return {
      flagText,
      changeFlag,
      ...toRefs(formInfo),
      formList,
      saveInfo,
    }
  }
};
</script>