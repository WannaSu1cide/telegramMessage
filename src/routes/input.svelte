    <script>
    import { each } from "svelte/internal";
      import { messages ,messageImage } from "./store";
      import { onMount } from "svelte";
      let inputValue = "";
      export  let takeUserUsing ;
      export  let chats = [];    
      let data = []
      let toggle = false;

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
        console.log($messages)
      }
      function addLikeIcon(event){
        console.log(event.target)
          $messages = [...$messages,event.target];
          $messageImage = [...$messageImage,result.img];
          console.log($messages)
      }
      const onKeyPress = (e) => {
        if (e.charCode === 13) {
          addVtoArray(inputValue);
        }        
      };
   
      function ShowEmoji(event) {
        inputValue += event.target.textContent;
  }
    </script>

    <main>
      <input
        type="text"
        class="input"
        bind:value={inputValue}
        on:keypress={onKeyPress}
        onblur="this.focus()" autofocus
        on:keydown={(event) => {
          if (event.key === "Enter") {
            addImageMessage();
          }
        }}
      />
      {#if toggle}
      <div class="emojiContainer">
        <div class="emojiSearch">

          <input type="text" class="searchEmoji">
        </div>
        <ul class="emojiWrap">
          {#each data as emoji}
            <li  on:click={ShowEmoji}>{emoji.character}</li>
          {/each}
        </ul>

      </div>
    {/if}
   <div class="Icon">
    <i class="fa-regular fa-face-smile smile" on:click={()=>{toggle =!toggle}} ></i>

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
    padding: 0;
    margin: 0;
    list-style-type: none;
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
