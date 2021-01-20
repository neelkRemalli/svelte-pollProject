<script>
import {createEventDispatcher} from 'svelte';
import  PollStore from '../store/pollStore.js'
import Button from '../shared/Button.svelte'
import {tweened} from 'svelte/motion';



const dispatch = createEventDispatcher();
export let poll
$: totalVotes = poll.votesA + poll.votesB;
$: barWidthA = Math.floor(100 / totalVotes * poll.votesA) || 0;
$: barWidthB = Math.floor(100/ totalVotes * poll.votesB)  || 0;

const tweenedA = tweened(0);
const tweenedB = tweened(0);
$:tweenedA.set(barWidthA);
$:tweenedB.set(barWidthB);



const addVotes = (option, id) =>{
    PollStore.update(currentPoll =>{
   
    let copiedPolls = [...currentPoll]
   
   let updatedPolls = copiedPolls.find(poll => poll.id === id)

   
   if(option === 'a'){
    updatedPolls.votesA++;
   }
   if(option === 'b'){
     updatedPolls.votesB++;
   }
   return copiedPolls;
})
    dispatch('handleVote', {option, id})
}

const handleDelete = (id) =>{
    
    PollStore.update(currentPoll =>{
      return  currentPoll.filter(poll => poll.id !== id)
        
    })
   
}

</script>


<div class='bg-white shadow-xl p-6 rounded-lg'>
    <h3 class='text-xl font-bold text-gray-700 '>{poll.question}</h3>
    <p class='text-xs my-1 font-bold'> Total Votes: {totalVotes}</p>

    <div class='bg-gray-300 rounded my-4 hover:bg-opacity-75 transition-all duration-500 relative border-l-4 border-red-600' on:click={()=>addVotes('a', poll.id)}>
        <div class='bg-red-500 h-full absolute  top-0 opacity-25 z-0' style='width:{$tweenedA}%'></div>
        <span class='px-4 py-4 inline-block font-bold text-gray-700 z-50'>{poll.answerA} ({poll.votesA})</span>
    </div>

    <div  class='bg-gray-300 rounded my-4 hover:bg-opacity-75 transition-all duration-500 relative  border-l-4 border-green-600' on:click={()=>addVotes('b', poll.id)} >
        <div class='bg-green-600 h-full top-0  opacity-25  absolute box-border' style='width:{$tweenedB}%'></div>
        <span class='px-4 py-4 inline-block font-bold text-gray-700 ' tyle>{poll.answerB} ({poll.votesB})</span>
    </div>
    <Button type='primary' on:click={handleDelete(poll.id)}>Delete</Button>
</div>