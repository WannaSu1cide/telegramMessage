<script>
  import Animation from "./animation.svelte";
  import Display from "./display.svelte";
  import { messages } from "./store";
  import Input from './input.svelte'
  import { onMount } from "svelte";
  export let chats = [];
 export let selectedChatId = 1;
  function selectChat(id) {
    selectedChatId = id;
  }
  // onMount(async () => {
	// 	const res = await fetch(`/dataUser.json`);
  //   console.log(res)
	// });
</script>

<div class="sidebar">
  {#each chats as chat}
    <div
      class={selectedChatId === chat.id ? "chat-item selected" : "chat-item"}
      on:click={() => selectChat(chat.id)}
    >
    <img class="avatar" src={chat.img} alt="Avatar" />

      <div class="name">{chat.name}</div>
    </div>
  {/each}

</div>
{#if $messages.length !== 0}
  <Display />
{:else}
  <Animation name={chats[selectedChatId - 1].name} />
{/if}
<Input chats={chats} takeUserUsing ={selectedChatId} />
<style>
  .sidebar {
    position: relative;
    width: 300px;
    background-color: #f5f5f5;
    border-right: 1px solid #e0e0e0;
    padding: 20px;
    overflow-y: auto;
    height: 100vh;
    margin: 0;
    left: 0;
    bottom: 0;
  }

  .chat-item {
    display: flex;
    align-items: center;
    padding: 10px;
    cursor: pointer;
    
  }

  .chat-item:hover {
    background-color: #ebebeb;
  }

  .selected {
    background-color: lightblue;
    color: white;
  }

  .chat-item .avatar {
    width: 40px;
    height: 40px;
    border-radius: 50%;
    object-fit: cover;
    margin-right: 10px;
  }

  .chat-item .name {
    font-weight: bold;
  }

</style>
