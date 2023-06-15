<script>
    import Sidebar from './sidebar.svelte'
 export let chats = [
    { id: 1, name: "Danh 1", img: "https://scontent.fsgn2-4.fna.fbcdn.net/v/t39.30808-6/295675909_992002361477789_5483028257691348362_n.jpg?_nc_cat=101&ccb=1-7&_nc_sid=174925&_nc_ohc=HyTgM-XJXnQAX-y5Sfw&_nc_ht=scontent.fsgn2-4.fna&oh=00_AfA6l7KN9rQG-m0fFTfTqQXJTTLN3E9OmpeUVgU4GaZS-A&oe=647E00C8"},
    { id: 2, name: "Danh 2", img: "https://scontent.fsgn2-3.fna.fbcdn.net/v/t39.30808-6/266905116_860927481251945_3820897564572505829_n.jpg?_nc_cat=107&ccb=1-7&_nc_sid=174925&_nc_ohc=KaWaTtEjt58AX9w0_EC&_nc_ht=scontent.fsgn2-3.fna&oh=00_AfD4F_iEW2ioyqNr8KZBZy2z-WRfY9s1zk-qiKpjmMJLqA&oe=647E0553"},
    { id: 3, name: "Danh 3", img: "https://scontent.fsgn2-5.fna.fbcdn.net/v/t39.30808-6/306864184_1023918421619516_4727217162646051818_n.jpg?stp=cp6_dst-jpg&_nc_cat=104&ccb=1-7&_nc_sid=8bfeb9&_nc_ohc=n22YmWewGdcAX8-EEzP&_nc_ht=scontent.fsgn2-5.fna&oh=00_AfC7s06ya9pfju5UmlpZvPT48Hq1oWCXdvKRNmBhJkIB2g&oe=647F2233"},
  ];

</script>
  <Sidebar {chats}/>
  


