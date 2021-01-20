<script>
    import Button from '../shared/Button.svelte'
    import {createEventDispatcher} from 'svelte'
    import  PollStore from '../store/pollStore.js'

    let dispatch = createEventDispatcher()
  let fields = {
    question: '',
    answerA: '',
    answerB: '',
  };
  let errors = {
    question: '',
    answerA: '',
    answerB: '',
  };
  let valid = false;

  const handleSubmit = () => {
   
   valid = true;
   if(fields.question.trim().length < 5){
     valid = false;
     errors.question = 'Question must be at least 5 length characters'
   }else{
     errors.question = ''
   }
   
   if(fields.answerA.trim().length < 1){
     console.log('answerA')
     valid = false;
     errors.answerA = 'answer A can not be empty'
   }else{
     errors.answerA = ''
   }
 
   if(fields.answerB.trim().length < 1){
     valid = false;
     errors.answerB = 'answer B can not be empty'
   }else{
     errors.answerB = ''
   }
   if(valid){
    let poll = {...fields, votesA: 0, votesB: 0, id: Math.random()}
    PollStore.update(currentPoll =>{
      return [poll, ...currentPoll]
    })
    dispatch('add')
   }
  };
</script>
<form on:submit|preventDefault="{handleSubmit}" class="w-1/2 mx-auto">
  <div class="my-5 text-gray-700">
    <label for="question">Poll Question:</label>
    <input
      class="border border-gray-500 outline-none block mt-3 p-2 w-full rounded"
      type="text"
      id="question"
      bind:value="{fields.question}"
    />
    <div class='text-red-600 text-center text-xs mt-1 font-bold'>{errors.question}</div>
  </div>
  <div class="my-5 text-gray-700">
    <label for="anwserA">Answer A:</label>
    <input
      class="border border-gray-500 outline-none block mt-3 p-2 w-full rounded"
      type="text"
      id="anwserA"
      bind:value="{fields.answerA}"
    />
    <div class='text-red-600 text-center text-xs mt-1 font-bold'>{errors.answerA}</div>
  </div>
  <div class="my-5 text-gray-700">
    <label for="anwserB">Answer B:</label>
    <input
      class="border border-gray-500 outline-none block mt-3 p-2 w-full rounded"
      type="text"
      id="anwserB"
      bind:value="{fields.answerB}"
    />
    <div class='text-red-600 text-center text-xs mt-1 font-bold'>{errors.answerB}</div>
  </div>
  <Button type='secondary'>Submit</Button>
</form>

<input />
<style></style>
