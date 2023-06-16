<script>
  import { messages, messageImage } from "./store";  
  const likeIcon =  `<i class="fa-regular fa-thumbs-up likeIcon"></i>`

</script>


<div class="container">
  <!-- render img and messages -->
  <div class="wrapAll">
    {#each $messageImage as img, i}
      {#if $messages[i]}
        <div class="wrap">
          <div class="wrapItem">
            <div class="wrapImg">
              <img src={img} alt="img " />
            </div>
            <div class="wrapMessage">
              <ul>
                <li>{$messages[i]}</li>
              </ul>
            </div>
          </div>
        </div>
      {/if}
    {/each}
  </div>
</div>



<style>
  .container {
    position: fixed;
    top: 0%;
    left: 20%;
    height: calc(100vh - 8%);
    width: 80vw;
    overflow-y: scroll;
    background-image: url("https://svgur.com/i/jyv.svg");
  }
  .wrapAll {
  display: flex;
  flex-wrap: wrap;
}

.wrap {
  flex: 0 0 100%;
}

.wrapItem {
  display: flex;
  align-items: flex-start;
}
.wrapMessage{
    overflow-wrap: break-word;
    max-width: 300px;
    background-color: #333;
    color:white;
    padding:5px 10px ;
    border-radius: 5px 10px 10px 5px;
    margin-top:2px;
    user-select: none;

 }

img {
  width: 30px;
  height: 30px;
  object-fit: cover;
  border-radius: 50%;
  margin-right: 10px;
}


ul {
  list-style-type: none;
  margin: 0;
  padding: 0;
}



  li {
    list-style-type: none;
  }

  @media only screen and (max-width: fullscreen) {
    .container {
      width: 60vw;
    }
  }
  @media only screen and (max-width: 1300px) {
    .container {
      width: 70vw;
      left: 32%;
    }
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
