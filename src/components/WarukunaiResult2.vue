<template>
  <div class="oyasumi-result">
    <div class="oyasumi-result_main">
      <img src="@/assets/waku_up.gif" alt>



      <div style="display: flex;align-items: stretch">
        <img src="@/assets/waku_left.gif" alt>
        <div class="oyasumi-result__message">

          <template v-for="(results, prevQuestionNumber2) in prevQuestionList">
            <p v-if="step2 > prevQuestionNumber2" :key="prevQuestionNumber2">
              <template v-for="(prevQuestion, resultIndex) in results">
                <span :key="prevQuestion" v-if="prevQuestions2[`q${prevQuestionNumber2+1}`] === resultIndex+1">{{'もとの文章：' + prevQuestion}}</span>
              </template>
            </p>
          </template>

        </div>


        <div class="oyasumi-result__message">
          <template v-for="(results, questionNumber2) in resultsList">
            <p v-if="step2 > questionNumber2" :key="questionNumber2">
              <template v-for="(result, resultIndex) in results">
                <span :key="result" v-if="answers2[`q${questionNumber2+1}`] === resultIndex+1">{{'アメリカン：' + result}}</span>
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
    prevQuestions2: Object,
    answers2: Object,
    step2: Number
  },

  computed: {
    prevQuestionList() {
      return [
        ['食事に出かけたら','仕事に行ったら','家から外を見てたら'],
        ['こんにちはと挨拶をした。','お世話になっておりますと言った。','いい天気ですねと言った。','黙って会釈をした。'],
        ['それからしばらく立ち話した。','話すこともないのですぐに帰った。','盛り上がったので飲みに行った。','という夢だった。']
      ]
    },
    resultsList() {
      return [
        //アメリカンジョーク
        ['きょうはハイウェイを飛ばしてハンバーガーを食べに行ったのさ。',
        'まったくこんな日に仕事とはついてないぜ、そう思って出かけたのさ。',
        'こんなゴキゲンな日は家でニートとしゃれ込んで窓から外を歩く人を見ていたのさ。'],

        ['それでおれは言ってやったのさ。「おいおい、シカ狩りにでも行く気かい？」ってね。',
        'だからおれは言ってやったのさ。「例のオイスターバーにはいつ連れてってくれるんだい？」ってね。',
        'だからおれは言ってやったのさ。「ハロウィンとクリスマスがいっしょにきたかのような空ですね」ってね。',
        '「３つ数えるうちに消え失せろ」って言ってやりたかったけど、あいにくホットドッグを食べていたんで念じただけさ。'],

        ['そしたらなんて言ったと思う？　「おあいにくさま。うちはもう間に合ってます」ですってよ。傑作だと思わなジョー',
        'そしたらなんて言ったと思う？　「私もそう思ってたんですけどどうして分かったんですか？」だってさ。そう言い終わらうちに慌てて帰ったね。',
        'そしたらなんて言ったと思う？　「それはうちの主人じゃなくてうちの犬ですわ」って。それからバーボン片手に3時間つきあうはめになったさ。',
        '「ゲロゲロゲロゲロ」ってカエルの鳴きまねさ。これはおかしいなと思ったら夕方。ソファーで寝てたって寸法さ。'],
      ]
    }
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