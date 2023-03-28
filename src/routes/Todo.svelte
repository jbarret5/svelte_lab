<script>
import Page from "./+page.svelte";

     let todoItem = '';
     let todoList = [];

     function add() {
          if (todoItem == ''){
               return;
          }
          todoList = [...todoList, {
               text: todoItem,
               done: false
          }]
          todoItem = '';
     }
     
     function removeThis(index) {
          todoList.splice(index, 1);
          todoList = todoList;
     }

     function clearDone(){
          todoList = todoList.filter(t => !t.done);
     }

     function clearAll(){
          todoList = [];
     }
</script>

<form on:submit|preventDefault={add}>
     <input class="blank" bind:value={todoItem} type="text" autofocus/>
     <button type="submit">Add</button>
</form>

<ul>
     {#each todoList as item, index}
          <li>
               <input type="checkbox" bind:checked={item.done}>
               <span class:done={item.done}>{item.text}</span>
               <span on:click={() => removeThis(index)} on:keypress={() => removeThis(index)} class="remove"></span>
          </li>
     {/each}
</ul>

<div class="clearBtn">
     <button on:click={clearDone}>Clear Done</button>
     <button on:click={clearAll}>Clear All</button>
</div>

<style>
     ul {
          list-style: none;
          font-size: 1.5vw;
          width: 399px;
          margin: auto;
          padding-bottom: 1vw;
          padding-top: 0.5vw;
     }
     .done {
          text-decoration: line-through;
          color: grey;
     }
     .remove {
          height: 2rem;
          width: 2rem;
          display: inline-block;
          background: url('./images/recycling-bag.png');
          background-size: 100% auto;
          cursor: pointer;
     }
     .blank {
          font-size: xx-large;
     }
     button{
          font-size: x-large;
          background-color: pink;
          color: rgb(218, 30, 61);
          border-radius: 3rem;
          padding: 0.7vw;
          border-color: rgb(218, 30, 61);
     }
     form{
          width: 500px;
          margin: auto;
     }
     .clearBtn{
          width: 399px;
          margin: auto;
     }
</style>