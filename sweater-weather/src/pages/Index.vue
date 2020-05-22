<template>
  <q-page class="flex column">
    <div class="col q-pt-lg q-px-md">
     <q-input
        class="fontColor"
        v-model="search"
        placeholder="Search"
        borderless
        dark>
        <template v-slot:before>
          <q-icon name="my_location" />
        </template>
        <template v-slot:hint>
          Field hint
        </template>

        <template v-slot:append>
          <q-btn round dense flat icon="search" />
        </template>
      </q-input>
    </div> 
    <div class="col text-white text-center">
        <div class="text-h4 text-weight-light">
          Philadelphia
        </div>
        <div class="text-h6 text-weight-light">
          Rain
        </div>
        <div class="text-h1 text-weight-thin q-my-lg relative-position">
         <span>34</span>
         <span class="text-h4 relative-position degrees">&deg;</span> 
        </div>
    </div>
  <div class="col text-center">
    <img src="https://www.fillmurray.com/100/100" alt="Billy">
  </div>
  <div class="col explore">

  </div>
  </q-page>
</template>

<script>
export default {
  name: 'PageIndex',
  data(){
    return{
      search: '',
      weatherData: null,
    }
  }
}
</script>
<style lang="sass">
  .q-page  
      background: linear-gradient(to bottom, #000428, #004e92)
  .fontColor
      color: white
  .degrees
      top: -42px
  .explore
      flex: 0 0 100px
      background: url(../statics/nyc2.png)
      background-size: contain
      background-position:center bottom

</style>