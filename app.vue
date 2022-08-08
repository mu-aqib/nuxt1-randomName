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

    generatedName.value = element.map(name => {
      return name.name
    })
  }
</script>
<template>
  <div class="container">
    <h1>Baby Name Generator</h1>
    <p>Choose your options and click the "Find Names" buttom below</p>

    <div class="options-container mb-3">
      <div class="option-container">
        <h4>1) Choose a gender</h4>

        <div class="option-buttons">
          <button class="option option-left" :class="options.gender === Gender.BOY && 'option-active'"
            @click="options.gender = Gender.BOY">
            Boy
          </button>
          <button class="option" :class="options.gender === Gender.UNISEX && 'option-active'"
            @click="options.gender = Gender.UNISEX">
            Unisex
          </button>
          <button class="option option-right" :class="options.gender === Gender.GIRL && 'option-active'"
            @click="options.gender = Gender.GIRL">
            Girl
          </button>
        </div>
      </div>

      <div class="option-container">
        <h4>2) Choose the name's popularity</h4>
        <div class="option-buttons">
          <button class="option option-left" :class="options.popularity === Popularity.TRENDY && 'option-active'"
            @click="options.popularity = Popularity.TRENDY">
            Trendy
          </button>
          <button class="option option-right" :class="options.popularity === Popularity.UNIQUE && 'option-active'"
            @click="options.popularity = Popularity.UNIQUE">
            Unique
          </button>
        </div>
      </div>

      <div class="option-container">
        <h4>2) Choose name's length</h4>
        <div class="option-buttons">
          <button class="option option-left" :class="options.length === Length.LONG && 'option-active'"
            @click="options.length = Length.LONG">
            Long
          </button>
          <button class="option" :class="options.length === Length.ALL && 'option-active'"
            @click="options.length = Length.ALL">
            All
          </button>
          <button class="option option-right" :class="options.length === Length.SHORT && 'option-active'"
            @click="options.length = Length.SHORT">
            Short
          </button>
        </div>
      </div>

      <button class="primary" @click="filterName">Find Names</button>

    </div>

    <table class="table">
      <thead>
        <th>S.No</th>
        <th>Name</th>
      </thead>
      <tbody>
        <tr v-for="(name, index) in generatedName" :key="index">
          <td data-label="S.No"> {{index}} </td>
          <td data-label="Name"> {{name}} </td>
        </tr>
      </tbody>
    </table>

  </div>
</template>

<style scoped>
  @import url('@/assets/style.css');
</style>