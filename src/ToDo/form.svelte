<script>
  export let task;
  export let taskDate;
  export let addTask;
</script>

<div>
  <h1>To Do List</h1>
</div>

<div class="parent">
  <div class="child">
    <input
      type="text"
      style="padding: 15px 150px;"
      placeholder="Add Your Task Here"
      bind:value={task}
      on:keypress={(event) => {
        if (event.key == "Enter") {
          addTask();
          task = "";
        }
      }}
      required
    />
  </div>

  <div class="child">
    <input
      type="date"
      style="padding: 15px 15px;"
      bind:value={taskDate}
      on:keypress={(event) => {
        if (event.key == "Enter") {
          addTask();
          task = "";
          taskDate = "";
        }
      }}
      required
    />
  </div>
</div>
