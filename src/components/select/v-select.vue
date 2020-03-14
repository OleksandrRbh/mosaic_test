<template>  
  <div class="v-select">
    <p
      class="title"
      @click="areOptionsVisible = !areOptionsVisible"
    >{{ selected }}</p>
    <div
      class="options"
      v-if="areOptionsVisible"
    >
      <p
        class="options__item"                
        v-for="option in options"
        :key="option.value"
        @click="selectOption(option)" 
      >
        {{ option.name }}
      </p>
    </div>
  </div>
</template>

<script>

export default {
  name: 'v-select',
  components: {},
  props: {
    options: {
      type: Array,
      default() {
        return []
      }
    },
    selected: {
      type: String,
      default: '' 
    }
  },
  data() {
    return{
      areOptionsVisible: false
    }
  },
  methods: {
    selectOption(option) {
      this.$emit('select', option);
      this.areOptionsVisible = false;      
    },
    hideSelect() {
      this.areOptionsVisible = false;
    }
  },
  mounted() {
    document.addEventListener('click', this.hideSelect.bind(this), true)
  },
  beforeDestroy(){
    document.removeEventListener('click', this.hideSelect)
  }
}
</script>

<style lang="scss">
  .v-select {
    position: relative;
    width: 200px;
    margin: 20px;
    cursor: pointer;

    p {
      margin: 0;      
    }

    .title {
      height: 30px;
      display: flex;
      align-items: center;
      justify-content: center;
      border: 1px solid #aeaeae;
    }

    .options {
      position: absolute;      
      top:31px;
      right: 0;
      width: 100%;
      height: 150px;
      box-sizing: border-box;
      overflow-y: scroll;
      border: 1px solid #aeaeae;
      background-color: #ffffff;
    }

    .options__item {
      padding: 5px 5px;
    }

    .options>p:hover {
      background-color: #eaeaea;
    }
  }
</style>