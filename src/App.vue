<template>
  <div id="app">


    <template>
    <!-- あなたは悪くない -->
    <RadioQuestion 
      key="radio1"
        v-if="step === 0"
        v-model="questions.q1"
        @next="handleNext"
        :questions="radioQuestionList[0]"
        :choices="radioQuestionList2[0]"
    />

    <RadioQuestion 
      key="radio2"
        v-if="step === 1"
        v-model="questions.q2"
        @next="handleNext"
        :questions="radioQuestionList[1]"
        :choices="radioQuestionList2[1]"
    />

    <RadioQuestion 
      key="radio3"
        v-if="step === 2"
        v-model="questions.q3"
        @next="handleNext"
        :questions="radioQuestionList[2]"
        :choices="radioQuestionList2[2]"
    />
    </template>

    <WarukunaiResult
      :step="step"
      :prevQuestions="questions"
      :answers="questions"

    />

    <template>
    <!-- アメリカンジョーク -->
    <RadioQuestion2
      key="radio4"
        v-if="step2 === 0"
        v-model="questions.q4"
        @next="handleNext2"
        :questions="radioQuestionList3[0]"
        :choices2="radioQuestionList4[0]"
    />

    <RadioQuestion2
      key="radio5"
        v-if="step2 === 1"
        v-model="questions.q5"
        @next="handleNext2"
        :questions="radioQuestionList3[1]"
        :choices2="radioQuestionList4[1]"
    />

    <RadioQuestion2
      key="radio6"
        v-if="step2 === 2"
        v-model="questions.q6"
        @next="handleNext2"
        :questions="radioQuestionList3[2]"
        :choices2="radioQuestionList4[2]"
    />

    </template>

    <WarukunaiResult2
      :step2="step2"
      :prevQuestions2="questions"
      :answers2="questions"
    />


  </div>
</template>

<script>
import RadioQuestion from './components/RadioQuestion.vue'
import RadioQuestion2 from './components/RadioQuestion2.vue'
import WarukunaiResult from './components/WarukunaiResult.vue'
import WarukunaiResult2 from './components/WarukunaiResult2.vue'
import { parse } from 'querystring'

export default {
  name: 'app',
  data() {
    return {
      step: 0,
      step2: 0,
      questions: {
        q1: 1, // あなたは悪くない
        q2: 1, // あなたは悪くない
        q3: 1, // あなたは悪くない
        q4: 1, // アメリカンジョーク
        q5: 1, // アメリカンジョーク
        q6: 1, // アメリカンジョーク
      },
    }
  },
  components: {
    RadioQuestion,
    RadioQuestion2,
    WarukunaiResult,
    WarukunaiResult2

  },
  mounted() {
    const params = parse(location.search.replace('?', ''))
    const isValid = ['q1', 'q2', 'q3', 'q4', 'q5', 'q6'].every((val) => {
      if (!params[val]) {
        return false
      }
      if (val != 'name' && parseInt(params[val]) < 1) {
        return false
      }
      return true
     })

    if (isValid) {
      const questions = {
        q1: parseInt(params.q1),
        q2: parseInt(params.q2),
        q3: parseInt(params.q3),
        q4: parseInt(params.q4),
        q5: parseInt(params.q5),
        q6: parseInt(params.q6),
      }

      this.questions = questions
      this.step = 0
      this.step2 = 0
    }

    

  },
  methods: {
    handleNext() {
      this.step ++
    },
    handleNext2() {
      this.step2 ++
    }
  },

  
  computed: {
    // あなたは悪くない
    radioQuestionList() {
      return [
        '気になっていることはなんですか。以下の4つから選ぶといちいち次のページで選んだことに対して優しく返してくれます。',
        'それは、ほっておいたらどうなりますか',
        '気になりますか',
      ]
    },

    radioQuestionList2() {
      return [
        ['借りた本をブックオフに売った','１週間も会社をずる休みしている','上司に頼まれた仕事を放置している','思い出すのもいやなんです'],
        ['職を失う','殴られる','ひどく怒られる','予想がつかない'],
        ['夢でも見るぐらい気にしている','起きてる間、ずっとそれを考えている','ときどき思い出す','ぜんぜん忘れてるっすよ']
      ]
    },
    // アメリカンジョーク
    radioQuestionList3() {
      return [
        'きょうはなにをしてましたか',
        '誰かにあいましたか',
        'そのあとどうしました'
      ]
    },

    radioQuestionList4() {
      return [
        ['食事に出かけた','仕事に行った','ずっと家にいた'],
        ['こんにちは','お世話になっております','いい天気ですね','黙って会釈した'],
        ['しばらく立ち話した','そんなにもりあがらずにすぐに分かれた','意気投合して飲みに行った','全部夢だった']
      ]
    },

  },
  routes: [
    { path: '/html/aend.htm', component: WarukunaiResult},
    { path: '/html/wend.htm', component: WarukunaiResult2}
  ]

}
</script>

<style>
* {
  box-sizing: border-box;
}

#app {
  font-family: sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  max-width: 640px;
  font-size: 12px;
  padding: 0 50px;
}
</style>