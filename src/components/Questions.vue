<template>
    <div class="questions-ctr">
        <div class="progress">
            <div class="bar"  :style="{width:`${questionAnswerd/questions.length*100}%`}"></div>
            <div class="status">{{questionAnswerd}} out of {{questions.length}} questions answered</div>
        </div>
        <transition-group name="fade">
            <div class="single-question" v-for="(question,qi) in questions" :key="question.q" v-show="questionAnswerd===qi">
                <div class="question">{{question.q}}</div>
                <div class="answers" >
                    <div class="answer"
                     v-for="answer in question.answers"
                     :key="answer.text"
                     @click.prevent="selectAnswered(answer.is_correct)"
                     >{{answer.text}}</div>
    
                </div>
            </div>
        </transition-group>
    </div>
</template>

<script>
export default{
    props:['questions','questionAnswerd'],
    emits:['question-answered'],
    methods:{
        selectAnswered(is_correct){
            this.$emit('question-answered',is_correct)
        }
    }
}
</script>