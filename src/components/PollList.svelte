<script>
    import PollListItem from './PollListItem.svelte'
    import  PollStore from '../store/pollStore.js'
    import {fade, scale} from 'svelte/transition'
    import {flip} from 'svelte/animate';
    export let polls = [];

</script>

<div class='grid grid-cols-2 gap-4'>
 {#each $PollStore as poll (poll.id)}
 <div in:fade out:scale|local	animate:flip={{duration: 500}}>
     <PollListItem {poll}  />
 </div>
 {/each}   
</div>


