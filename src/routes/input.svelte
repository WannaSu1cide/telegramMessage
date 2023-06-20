    <script>
      import { messages ,messageImage } from "./store";
      import { onMount } from "svelte";
      import { clickOutside } from "./clickOutside"
      let inputValue = "";
      export  let takeUserUsing ;
      export  let chats = [];    
      let data = []
      let ShowEmojiContainer = false;
      let searchEmojiValue = "";

      let emojiFilter = [];
      $:console.log(emojiFilter)
      onMount(
        async ()=>{
        const res = await   fetch("https://emoji-api.com/emojis?access_key=ebce92b8e661a6ee7ab038c4253d32c309e83958")
          data = await res.json();
       		}     
      )
        
      
      $: result = chats[takeUserUsing-1];
      function addVtoArray(newMessage){
        if (newMessage != 0){
          newMessage.trim();
          $messages = [...$messages, newMessage];
          inputValue = "";
        }
      }
      function addImageMessage(){
        if(inputValue != ""){
          let dataImg = result.img;
          $messageImage = [...$messageImage,dataImg];
        }
      }
      function addLikeIcon(event){
        console.log(event.target)
          $messages = [...$messages,event.target];
          $messageImage = [...$messageImage,result.img];
      }
      const onKeyPress = (e) => {
        if (e.charCode === 13) {
          addVtoArray(inputValue);
        }        
      };
   
      function ShowEmoji(event) {
        inputValue += event.target.textContent;
  }
  const searchEmoji =  function(){
        return emojiFilter = data.filter(emoji =>{
             let emojiSubGroup = emoji.subGroup.toLowerCase();
          return emojiSubGroup.includes(searchEmojiValue.toLowerCase());
        })
    }
    </script>

    <main>
      <input
        type="text"
        class="input"
        bind:value={inputValue}
        on:keypress={onKeyPress}
          autofocus
          on:keydown={(event) => {
          if (event.key === "Enter") {
            addImageMessage();
          }
        }}
      />
      {#if ShowEmojiContainer}
      <div class="emojiContainer" use:clickOutside on:outclick={() => (ShowEmojiContainer = false)}>
        <div class="emojiSearch">
          <input type="text" class="searchEmoji" on:input={searchEmoji} bind:value={searchEmojiValue}> 
        </div>
        {#if searchEmojiValue !== "" }
        <ul class="filter">
        {#each emojiFilter as emoji}
        <li  on:click={ShowEmoji}>{emoji.character}</li>
        {/each}
        </ul>
          {:else}
        <ul class="emojiWrap">
          {#each data as emoji}
            <li  on:click={ShowEmoji}>{emoji.character}</li>
          {/each}
        </ul>
        {/if}
      </div>
      {/if}
   <div class="Icon">
    <i class="fa-regular fa-face-smile smile" on:click={()=>{ShowEmojiContainer = !ShowEmojiContainer}} ></i>
    <i class="fa-regular fa-thumbs-up likeIcon" on:click={addLikeIcon} ></i>
   </div>
    
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
    
  .emojiContainer{
    position: absolute;
    bottom: 110%;
    height: 600px;
    right: 5%;
    width: 500px;
    border: 1px solid;
    overflow: scroll;
    user-select: none;
    overflow-x: hidden;
    background-color: white;
    border-radius: 20px;
  }
  ul{
    display: flex;
    flex-wrap: wrap;
    list-style-type: none;
  }
  .filter{
    display: flex;
  }
      .emojiContainer li{
        list-style-type: none;
        flex: 1;
        width: 100%;
        font-size: 30px;
      cursor: pointer;
  }
  .searchEmoji{
      width: 95%;
      margin-left:10px ;
      margin-top:10px;
      height: 50px;
      border-radius:20px;
      padding: 0 20px;
      font-size: 20px;
      outline: none;
      border: none;
      background-color: #333;
      color: white;
      z-index: 1;
      position: relative;
  }
  .Icon{
    position: inherit;
    top: 15px;
    right:0% ; 
    font-size: 30px;
    
  }
  
  .Icon > i {
    margin-right: 20px;
  }
  .likeIcon:hover{
    color:lightblue;

  }
  .smile:hover{
    color:lightblue;
    cursor: pointer;
  }
  ::-webkit-scrollbar {
    width: 5px;
  }

  /* Track */
  ::-webkit-scrollbar-track {
    background: #888;
  }

  /* Handle */
  ::-webkit-scrollbar-thumb {
    background: #333;
    border-radius: 20px;
    height: 10px;
  }

  /* Handle on hover */
  ::-webkit-scrollbar-thumb:hover {
    background: #555;
  }


    </style>
