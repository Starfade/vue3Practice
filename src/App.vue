<template>
  <nav>
    <router-link to="/">组合式api和计算属性</router-link> 
    <router-link to="/game">色块小游戏</router-link> 
    <router-link to="/element">elementPlus尝试</router-link> 
  </nav>
  <router-view/>
</template>

<style lang="less">
*{
  padding: 0;
  margin: 0;
}
nav {
  display: flex;
  justify-content: space-around;
  flex-wrap: wrap;
  width: 100%;
}
</style>
