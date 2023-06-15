  <script>
  import { each } from "svelte/internal";
    import { messages ,messageImage } from "./store";
    import { onMount } from "svelte";
    let inputValue = "";
    export  let takeUserUsing ;
    export  let chats = [];    
    let data = []

    onMount({
      async function (){
      const res = await   fetch("https://emoji-api.com/emojis?access_key=ebce92b8e661a6ee7ab038c4253d32c309e83958")
        data = await res.json();
      console.log(data);
      }
    })
    function onInput(event){
         inputValue = event.target();
    }
    $: result = chats[takeUserUsing-1];
    function addVtoArray(newMessage){
      if (newMessage != 0){
        newMessage.trim();
        $messages = [...$messages, newMessage];
        inputValue = "";
      }
    }
    function addImageMessage(){
      if(inputValue!= ""){
        let dataImg = result.img
        console.log(dataImg)
        $messageImage = [...$messageImage,dataImg];
      }
    }
    const onKeyPress = (e) => {
      if (e.charCode === 13) {
        addVtoArray(inputValue);
      }
    };
    let toggle = false;

  </script>

  <main>
    <input
      type="text"
      class="input"
      bind:value={inputValue}
      on:keypress={onKeyPress}
      on:keydown={(event) => {
        if (event.key === "Enter") {
          addImageMessage();
        }
      }}
    />
  
    <button
      on:keypress = {addImageMessage}
      on:click={addVtoArray(inputValue)}
      on:click ={addImageMessage}
      on:input= {onInput}
    >
      <i class="fa-regular fa-paper-plane plane" />
    </button>

    <i class="fa-regular fa-face-smile smile "></i>
    {#if toggle}
      <div class="emojiContainer">
        <div class="emojiSearch"></div>
        <ul class="emojiWrap">
          {#each data as emoji}
            <li>{emoji.character}</li>
          {/each}
        </ul>
      </div>

    {/if}



  </main>

  <style>
    main {
      position: absolute;
      bottom: 0;
      right: 0;
      height: 8%;
      width: calc(100vw - 300px);
      border: none;
    }
    .input {
      position: absolute;
      bottom: 0;
      width: 100%;
      height: 100%;
      font-size: 15px;
      padding: 0px 10% 0 25px;
    }
 
    button {
      position: inherit;
      right: 2%;
      bottom: 15%;
      font-size: 25px;
      border: none;
      background-color: white;
      cursor: pointer;
    }
    .buttonContainWords {
      color: lightblue;
    }


 
  </style>
