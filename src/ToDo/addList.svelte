<script>
  export let i;
  export let item;
  export let removeFromList;
</script>

<div class="parent">
  <div class="child">
    <input class="larger" bind:checked={item.status} type="checkbox" />
    <span class:checked={item.status}>📝{item.task} </span>
  </div>

  <div class="child">
    <span class:checked={item.status}>
      {item.daysLeft}Days {item.hoursLeft}Hrs⌛</span
    >
  </div>
  <div class="child">
    <span class:checked={item.status}>{item.taskDate} </span>
    <!-- svelte-ignore a11y-click-events-have-key-events -->
    <span class="removeDiv" on:click={() => removeFromList(i)}>❌</span>
  </div>
</div>