<script>
    import Sidebar from './sidebar.svelte'





 export let chats = [
    { id: 1, name: "Danh 1",img:"/img1.jpg"},
    { id: 2, name: "Danh 2",img:"/img2.jpg"},
    { id: 3, name: "Danh 3",img:"/img3.jpg"},
  ];
</script>
  <Sidebar {chats}/>
  
  


