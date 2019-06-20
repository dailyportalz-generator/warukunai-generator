<template>
  <div class="oyasumi-result">
    <div class="oyasumi-result_main">
      <img src="@/assets/waku_up.gif" alt>
      <div style="display: flex;align-items: stretch">
        <img src="@/assets/waku_left.gif" alt>

        <div class="oyasumi-result__message">

          <template v-for="(results, prevQuestionNumber) in prevQuestionList">
            <p v-if="step > prevQuestionNumber" :key="prevQuestionNumber">
              <template v-for="(prevQuestion, resultIndex) in results">
                <span :key="prevQuestion" v-if="prevQuestions[`q${prevQuestionNumber+1}`] === resultIndex+1">{{'--- ' + prevQuestion}}</span>
              </template>
            </p>
          </template>

        </div>


        <div class="oyasumi-result__message">

          <template v-for="(results, questionNumber) in resultsList">
            <p v-if="step > questionNumber" :key="questionNumber">
              <template v-for="(result, resultIndex) in results">
                <span :key="result" v-if="answers[`q${questionNumber+1}`] === resultIndex+1">{{result}}</span>
              </template>
            </p>
          </template>

        </div>

        <img src="@/assets/waku_left.gif" alt>
      </div>
      <img src="@/assets/waku_down.gif" alt>
    </div>
  </div>

  
</template>

<script>/*
import { stringify } from 'querystring'*/
export default {
  props: {
    prevQuestions: Object,
    answers: Object,
    step: Number
  },

  computed: {
    prevQuestionList() {
      return [
        //あなたは悪くない
        ['借りた本をブックオフに売った','１週間も会社をずる休みしている','上司に頼まれた仕事を放置している','思い出すのもいやなんです'],
        ['職を失う','殴られる','ひどく怒られる','予想がつかない'],
        ['夢でも見るぐらい気にしている','起きてる間、ずっとそれを考えている','ときどき思い出す','ぜんぜん忘れてるっすよ']
      ]
    },
    resultsList() {
      return [
        //あなたは悪くない
        ['借りた本を売ってしまうなんてよくあることです。読まなくなった本がもったいない。リサイクルをしようとしたあなたは倫理感の強い人なんです。',
        '仕事を休んでいるんですね。「ずる」でもなんでもなくて、あなたは行きたくないから行かないんですよね。自分に正直なんですよ。',
        'やっかいな仕事を引き受けてしまったんですよね。もしかしたらうまいこと言って別の人におしつけることもできたかもしれない。それをしなかったのがあなたのいいところです。',
        '人に言える悩みなんて悩みじゃないですよね。書くことができないという自分の状態を把握できているなんてなかなかないことです。'],
        
        ['職を失うほどの大事なこと。逆に言えばそんなたいせつなものに関わっているなんてあなたが信頼されていることの証拠にほかなりません。',
        'あなたには暴力でしか表現できない人の感情を受け止める度量の広さがあるのです。まさに現代のガンジーです！',
        '怒られるだろうな、という予測ができているのは先の見通しができているということに他なりません。先見の明があると言ってもいいでしょう。もっと自信を持って！',
        '予想は外れるもの。予想がつかないといういいかたがいちばん正解なんです。そんな真理を言い当てるなんてあたなすごいですよ！'],
        
        ['忘れてることにしたいけど気にしているのではないでしょうか。大胆に見られることが多いあなたですが、実は繊細なんですよね。そういう誤解を受けることも多いでしょう。',
        '自信家に見られがちなあなたですが、内面は弱いところがあります。私にはわかります。夢に出て当然ですよ。',
        '常にそのことを考えて解決策を練っている。あなたの前向きさを物語っていると思います。',
        '本当にときどきなんでしょうか。もしかしたらずっと気になっているのかもしれません。でも忘れようとする、その葛藤を知っていることがあなたの誠実さです。'],
      ]
    },
  },
  methods: {
    handleClickRestart() {
      location.href = location.href.replace(location.search, '')
    }
  }
}
</script>

<style scoped>
img {
  user-select: none;
}
.oyasumi-result {
  width: 526px;
  margin: 0 auto;
}
.oyasumi-result_main {
  font-size: 0;
}
.oyasumi-result__message {
  padding: 16px;
  font-size: 12px;
  flex: 1;
  min-height: 150px;
}
.oyasumi-result__message p:first-child {
  margin-top: 0;
}
.oyasumi-result_build {
  text-align: right;
}
.oyasumi-result_share {
  font-size: 12px;
}
.oyasumi-result_shareurl {
  width: 100%;
}
.oyasumi-result_share {
  display: flex;
  align-items: center;
}
input {
  margin: 4px 10px 4px 0;
  flex: 1;
}
</style>