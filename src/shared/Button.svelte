<script>
export let type ='primary';
export let flat= true;
</script>


<button class="bg-blue-500 mt-4 text-white px-8 py-2 rounded text-lg font-bold focus:outline-none {type}" class:flat={flat} on:click >
    <slot></slot>
  </button>

  <style>
      .primary{
          background: #DC2626;
      }
      .secondary{
          background: #10B981;
      }
      .flat{
          box-shadow: 0px 0px 4px rgba(0, 0, 0, .50);
      }
  </style>