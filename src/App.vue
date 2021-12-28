<template>
  <div id="app">
    <header>
      <a href="https://decimodan.com">
        <img src="@/assets/logo.png"/>
      </a>
      <nav>
          <ul>
            <li>
              <router-link to='/'>Inicio</router-link>
            </li>
            <li>
              <router-link to='/calculadora'>Calculadora</router-link>
            </li>
            <!-- <li>
              <router-link to='/about'>Acerca</router-link>
            </li> -->
          </ul>
        </nav>
    </header>
    <router-view/>
  </div>
</template>

<script>
</script>

<style>
body {
  margin: 0;
  /* background-color: #020C0E; */
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
header img {
    height: 40px;
    margin-left: 40px;
}
body {
    font-family: sans-serif;
    margin-top: 100px;
}

main {
  color: white;
  text-align: center;
  margin-top: 40px;
}

header {
    background-color: #1e3757;
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    height: 80px;
    display: flex;
    align-items: center;
    box-shadow: 0 0 2px 0 #020C0E;
}

header * {
    display: inline;
}

header li {
    margin: 20px;
}

header li a {
    color: white;
    text-decoration: none;
    font-weight: bold;
}

header span {
  display: block;
  position: relative;
  font-size: 20px;
  line-height: 1;
  letter-spacing: .02em;
  font-weight: 400;
  box-sizing: border-box;
  padding-top: 16px;
}
</style>