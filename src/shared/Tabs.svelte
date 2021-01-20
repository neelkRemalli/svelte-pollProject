<script>
 
 import {createEventDispatcher } from 'svelte';
 const dispatch = createEventDispatcher();
  export let items;
  export let activeItem;
</script>
<div class='tab'>
  <ul>
    {#each items as item}
    <li class:active={item === activeItem} 
     on:click={()=>dispatch('tabChange', item)}
    >
      <div>{item}</div>
    </li>
    {/each}
  </ul>
</div>

<style>
.tab{
    margin-bottom: 40px;
    color: #777;
}
ul{
    display: flex;
    justify-content: center;
}
li{
    list-style-type: none;
    margin: 0 15px;
    font-size: 20px;
    font-weight: 500;
    display: inline-block;
    cursor: pointer;
}
.active{
    color: #DC2626;
    border-bottom: 2px solid #DC2626;
    padding-bottom: 4px;

}
</style>
