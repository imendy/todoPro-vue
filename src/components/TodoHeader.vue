<script setup>
  import { RouterLink } from 'vue-router';
</script>

<template>
<header>
    <nav class="container">
        <div class="branding">
            <h1>TodoPro</h1>
            <img src="../assets/todo-logo.png" alt="">
        </div>

        <ul class="nav-routes">
            <RouterLink to="/">
               Home
             </RouterLink>

             <RouterLink to="/about">
               About
             </RouterLink>
        </ul>
        
    </nav>
</header> 
</template>


<style lang="scss" scoped>

:root {
  --transition-duration: 0.7s;
}

header {
  background-color: #f1f1f1;
  nav {
    display: flex;
    align-items: center;
    padding: 25px 16px;

    .branding {
      display: flex;
      align-items: center;
      gap: 8px;
      img {
        max-width: 35px;
      }

      h1 {
        font-size: 13px;
      }
    }

    .nav-routes {
     display: flex;
     flex: 1;
      justify-content: flex-end;
       gap: 12px;
      list-style: none;
       font-weight: 500;

  a {
    text-decoration: none;
    color: inherit;

    &:hover {
      transform: translateY(2px);
      transition: transform var(--transition-duration, 0.3s) ease;
    }
  }
}


  }
}
</style>