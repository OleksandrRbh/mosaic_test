<template>  
  <div class="v-table-row">
    <div class="row row__first-name">{{row_data.firstname}}</div>
    <div class="row row__last-name">{{row_data.lastname}}</div>
    <div class="row row__email">{{row_data.email}}</div>
    <div class="row row__phone">{{row_data.phonenumber}}</div>
    <div class="row row__birthday">{{row_data.birthday_contact}}</div>
    <div class="row row__company">{{row_data.company}}</div>
  </div>
</template>

<script>
export default {
  name: 'v-table-row',  
  props: {
    row_data: {
      type: Object,
      default: () => {
        return {}
      }
    }
  },
  data() {
    return{}
  },
  computed: {}
}
</script>

<style lang="scss">
  .v-table-row {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center; 

    .row {
      text-align: left;
      padding: 8px 16px;
      flex-basis: 16%;
    }
  }
</style>