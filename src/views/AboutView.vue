<template>
  <div class="about">
      Welcome to my Todo application built with Vue.js 3! The purpose of this
      app is to help users manage their tasks and stay organized in a simple and
      intuitive way. Whether you need to keep track of your work assignments,
      personal projects, or daily errands, this app has got you covered.
  </div>
</template>

<style lang="scss" scoped>
.about {
  font-size: 29px;
  width: 100%;
  display: flex;
  padding: 20rem;
  align-items: center;
  justify-content: center; 
  @media screen and (max-width: 1024px) {
    padding: 20px;
  }
 }
</style>
