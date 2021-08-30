<template>
  <div id="app" v-cloak>
    <div class="display" v-show="!showEnd">
      <h1>Who Wants To Be A Milionare</h1>
      <div id="que">
        <h3> {{ questions[indexQ].question}} </h3>
      </div>
      <div id="ans">
        <div v-for="(answer, index) in questions[indexQ].answers" :key="index"
          :class="{'show-correct-answer': showCorrectAnswer && questions[indexQ].correct == index,
                  'blink': blink && chosenAnswer == index}"
          @click="chosenAnswer = index; showAnswer();" >
          {{ answer }}
        </div>
      </div>
    </div>
    <div class="endGame" :class={display:showEnd}>
      <h1 v-show="showEnd && win"> You Win </h1>
      <h1 v-show="showEnd && !win"> You Lose </h1>
    </div> 
  </div>
</template>

<script>

export default {
  data(){
    return {
      questions: [
        {
          question: "Em muốn người yêu đào hoa ?",
          answers: ['A. Phải', 'B. Không', 'C. Không', 'D. Không'],
          correct: 0
        },
        {
          question: "Em muốn anh ta chung thủy ? ",
          answers: ['A. Không', 'B. Phải', 'C. Không', 'D. Không'],
          correct: 1
        },
        {
          question: "Em thích một kẻ phóng khoáng nhưng phải biết chi li từng tí ",
          answers: ['A. Không', 'B. Không', 'C. Phải', 'D. Không'],
          correct: 2
        },
        {
          question: "Em muốn một người cho em không gian riêng, nhưng luôn biết là em cần gì ? ",
          answers: ['A. Không', 'B. Không', 'C. Không', 'D. Phải'],
          correct: 3
        }
      ],
      indexQ: 0,
      chosenAnswer: null,
      timer1: null,
      timer2: null,
      blink: false,
      showCorrectAnswer: false,
      showEnd: false,
      win: true,
      maxQuestion: 4
    }
  },
  methods: {
    showAnswer: function(){
      this.blink = true;

      this.timer1 = setInterval(() => {
        this.blink = false;
        this.showCorrectAnswer = true;
        clearInterval(this.timer1);
      }, 2000);
      
      if (this.chosenAnswer == this.questions[this.indexQ].correct) {
        this.timer2 = setInterval(()=>{
        this.chosenAnswer = null;
        this.showCorrectAnswer = false;
        clearInterval(this.timer2);
        if(this.indexQ == this.maxQuestion - 1) this.showEnd = true;
        else{
          this.indexQ++;
        }
      }, 4000)}

      else {
        this.showEnd = true;
        this.win = false;
      }
    }
  }
}
</script>
<style>
.display{
  width: 600px;
  height: 350px;
  margin: 0 auto;
  background-color: rgb(20, 13, 109);;
}
.display > h1 {
  color: wheat;
  text-align: center;
  padding-top: 20px;
}
.endGame > h1 {
  color: yellow;
  line-height: 250px;
}
#que {
  border: 5px yellowgreen solid;
  border-radius: 30px;
  width: 80%;
  margin: 0 auto;
}
#que > h3 {
  color: wheat;
  padding: 0 20px;
  text-align: center;
}
#ans {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  width: 80%;
  margin: 30px auto;

}
#ans > div {
  width: 180px;
  border: 3px yellowgreen solid;
  border-radius: 20px;
  height: 30px;
  color: wheat;
  line-height: 30px;
  margin: 10px;
  padding-left: 20px;
  cursor: pointer;
}
.show-correct-answer{
  background-color: #52AF21 !important;
}
.blink {
  animation: blink 0.3s linear 8;
}
.choose-answer {
  background-color: #F17B03;
}
@keyframes blink {
  from {background: transparent;} to {background: #F17B03;}
}
</style>
