<template>
  <form @submit.prevent="handleSubmit" class="select-question">

    <!-- 質問 -->
    <p>{{questions}}</p>
    <div>
        <!-- あなたは悪くない選択肢 -->
        <template v-for="(label,i) in choices">
          <label :key="label">
            <input type="radio" name="question" :value="i+1" v-model="pick" :key="label">
            {{ label}}
          </label><br>
        </template>


    </div>
    <button>次へ</button>
  </form>


</template>

<script>
export default {
  props: {
    questions: String,
    choices: Array
  },
  data() {
      return {
          pick: 0
      }
  },

  methods: {
      handleSubmit() {
          this.$emit('next')
          this.$emit('input', this.pick) //選択されたラジオボタン情報をApp.vueに引き渡す

      },
  }


}
</script>

<style scoped>
.select-question {
  margin-bottom: 24px;
  padding-bottom: 24px;
  border-bottom: dotted 1px #c6c6c6;
}

h3 {
  font-size: 1em;
}

dd {
  margin: 16px 0 0;
  padding: 0 0 8px 0;
}

button {
  width: 60px;
}

input[type='text'] {
  margin-right: 20px;
}
</style>