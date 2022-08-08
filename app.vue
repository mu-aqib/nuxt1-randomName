<script setup lang="ts">
  import {
    Gender,
    Popularity,
    Length,
    names
  } from '@/data'

  interface OptionsState {
    gender: Gender,
      popularity: Popularity,
      length: Length
  }

  const options = reactive < OptionsState > ({
    gender: Gender.BOY,
    popularity: Popularity.UNIQUE,
    length: Length.LONG
  })

  const generatedName = ref < String[] > ([])

  const filterName = () => {
    const element = names.filter(name => options.gender === name.gender)
      .filter(name => name.popularity === options.popularity)
      .filter(name => {
        if (options.length === Length.ALL) return true
        else return name.length === options.length
      })

    generatedName.value = element.map(name => name.name)
    
  }

  // component data
  const OptionsArray = [{
      title: "Choose a gender",
      category: 'gender',
      buttons: [Gender.BOY, Gender.GIRL, Gender.UNISEX]
    },
    {
      title: "Choose the name's popularity",
      category: 'popularity',
      buttons: [Popularity.TRENDY, Popularity.UNIQUE]
    },
    {
      title: "Choose name's length",
      category: 'length',
      buttons: [Length.LONG, Length.SHORT, Length.ALL]
    }
  ]
</script>

<template>
  <div class="container">
    <h1>Baby Name Generator</h1>
    <p>Choose your options and click the "Find Names" buttom below</p>

    <div class="options-container mb-3">

      <Options v-for="option in OptionsArray" :key="option.title" :singleOption="option" :options="options" />

      <button class="primary" @click="filterName">Find Names</button>

    </div>

    <Table v-if="generatedName.length > 0" :generatedName="generatedName" />

  </div>
</template>

<style>
  @import url('@/assets/style.css');
</style>