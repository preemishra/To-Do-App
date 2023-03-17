<script>
  import AddList from "../ToDo/addList.svelte";

  var searchDate = "";
  let block = "";
  let task = "";
  let taskDate = "";
  let taskList = "";
  let today = new Date();
  let yesterday = new Date(today);
  yesterday.setDate(yesterday.getDate() - 1);
  let minDate = yesterday.toISOString().split("T")[0]; //convert in string & extract the date part
  function addTask() {
    task = task.trim();
    if (task === "") {
      return;
    }
    const now = new Date().getTime();
    const myTaskDate = new Date(taskDate).getTime();

    const timeLeft = myTaskDate - now;

    const daysLeft = Math.floor(timeLeft / (1000 * 60 * 60 * 24));
    const hoursLeft = Math.floor(
      (timeLeft % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60)
    );

    let taskObject = {
      status: false,
      task: task,
      daysLeft: daysLeft,
      hoursLeft: hoursLeft,
      taskDate: taskDate,
    };
    taskList = [...taskList, taskObject];
    block = "all";
    taskList.sort((a, b) => {
      let date1 = new Date(a.taskDate);
      let date2 = new Date(b.taskDate);
      return date1 - date2;
    });
  }
  function removeFromList(i) {
    taskList.splice(i, 1);
    taskList = taskList;
  }
</script>

<body>
  <div>
    <h1>To Do List</h1>
  </div>

  <div class="parent">
    <div class="child">
      <input
        type="text"
        style="padding: 15px 150px;"
        placeholder="What needs to be done?"
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
        min={minDate}
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

  <div>
    {#each taskList as item, i}
      {#if block === "all"}
        <AddList {i} {item} {removeFromList} />
      {:else if block === "completed" && item.status === true}
        <AddList {i} {item} {removeFromList} />
      {:else if block === "incomplete" && item.status === false}
        <AddList {i} {item} {removeFromList} />
      {:else if block === "date" && item.taskDate === searchDate}
        <AddList {i} {item} {removeFromList} />
      {/if}
    {/each}
  </div>

  <div class="parent">
    <button
      type="button"
      class="button"
      on:click={() => {
        block = "all";
      }}>Display All</button
    >
    <button
      type="button"
      class="button"
      on:click={() => {
        block = "completed";
      }}>Completed</button
    >
    <button
      type="button"
      class="button"
      on:click={() => {
        block = "incomplete";
      }}>Incomplete</button
    >
    <input
      type="text"
      class="button"
      placeholder="Search By Date"
      onfocus="(this.type = `date`)"
      bind:value={searchDate}
      on:change={() => {
        block = "date";
      }}
    />
  </div>
</body>
