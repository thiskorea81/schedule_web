<template>
  <div id="app">
    <header>
      <h1>My Personal Website</h1>
    </header>
    <menu>
      <nav>
        <ul>
          <li><a href="#">Home</a></li>
          <li><a href="#">About</a></li>
          <li><a href="#">Contact</a></li>
        </ul>
      </nav>
    </menu>
    <div class="main-content">
      <section>
        <h2>Welcome to My Personal Website</h2>
        <p>This is the main content area.</p>
      </section>
      <side>
        <SideBar />
      </side>
    </div>
    <footer>
      <p>&copy; 2024 My Personal Website</p>
    </footer>
  </div>
</template>

<script>
import SideBar from './components/SideBar.vue';

export default {
  name: 'App',
  components: {
    SideBar
  }
};
</script>

<style>
#app {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}
header {
  background-color: #42b983;
  color: white;
  padding: 10px;
  text-align: center;
}
menu {
  background-color: #333;
}
menu nav ul {
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;
  justify-content: center;
}
menu nav ul li {
  margin: 0 15px;
}
menu nav ul li a {
  color: white;
  text-decoration: none;
}
.main-content {
  display: flex;
  flex: 1;
}
side {
  background-color: #f4f4f4;
  padding: 20px;
  width: 300px;
}
section {
  flex: 1;
  padding: 20px;
}
footer {
  background-color: #333;
  color: white;
  text-align: center;
  padding: 10px;
}
</style>
