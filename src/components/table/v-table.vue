<template>    
  <div class="v-table">
    <div class="selects-wrapper">
      <v-select
        class="v-select"
        :options="months"
        @select="sortByMonth"
        :selected="selectedMonth"
      /> 
      <v-select
        class="v-select"
        :options="days"
        @select="sortByDay"
        :selected="selectedDay"
      />    
    </div>
    <div class="v-table__header">
      <p class="v-table__data">Firstname</p>
      <p class="v-table__data">Lastname</p>
      <p class="v-table__data">Email</p>
      <p class="v-table__data">Phonenumber</p>
      <p class="v-table__data">Birthday</p>
      <p class="v-table__data">Company</p>
    </div>
    <div class="v-table__body">
      <v-table-row 
        class="body__row"
        v-for="(row, index) in filteredUsers"
        :key="index"
        :row_data="row"
      />        
    </div>
    <p 
      v-if="!sortedUsersTotal.length"
      class="err-message"
    >По Вашему запросу ничего не найдено</p>
  </div>
</template>

<script>
import vTableRow from './v-table-row'
import vSelect from '../select/v-select'

export default {
  name: 'v-table',
  components: {
    vTableRow,
    vSelect
  },
  props: {
    users_data: {
      type: Array,
      default: () => {
        return []
      }
    }
  },
  data() {
    return{
      months: [
        {name: 'Все месяцы', value: 0},
        {name: 'Январь', value: 1},
        {name: 'Февраль', value: 2},
        {name: 'Март', value: 3},
        {name: 'Апрель', value: 4},
        {name: 'Май', value: 5},
        {name: 'Июнь', value: 6},
        {name: 'Июль', value: 7},
        {name: 'Август', value: 8},
        {name: 'Сентябрь', value: 9},
        {name: 'Октябрь', value: 10},
        {name: 'Ноябрь', value: 11},
        {name: 'Декабрь', value: 12}
      ],
      selectedMonth: 'Все месяцы',
      sortedUsersByMonth: [], 
      
      days: [
        {name: 'Все дни', value: 0},
        {name: '1', value: 1},
        {name: '2', value: 2},
        {name: '3', value: 3},
        {name: '4', value: 4},
        {name: '5', value: 5},
        {name: '6', value: 6},
        {name: '7', value: 7},
        {name: '8', value: 8},
        {name: '9', value: 9},
        {name: '10', value: 10},
        {name: '11', value: 11},
        {name: '12', value: 12},
        {name: '13', value: 13},
        {name: '14', value: 14},
        {name: '15', value: 15},
        {name: '16', value: 16},
        {name: '17', value: 17},
        {name: '18', value: 18},
        {name: '19', value: 19},
        {name: '20', value: 20},
        {name: '21', value: 21},
        {name: '22', value: 22},
        {name: '23', value: 23},
        {name: '24', value: 24},
        {name: '25', value: 25},
        {name: '26', value: 26},
        {name: '27', value: 27},
        {name: '28', value: 28},
        {name: '29', value: 29},
        {name: '30', value: 30},
        {name: '31', value: 31},
      ],
      selectedDay: 'Все дни',
      sortedUsersByDay: [], 

      sortedUsersTotal: [],
          
    }
  },
  watch: {
    users_data() {
      this.sortedUsersByMonth = [...this.users_data];
      this.sortedUsersByDay = [...this.users_data];
    },
    sortedUsersByMonth(){     
      this.sortedUsersTotal = [];
      for (let item of this.sortedUsersByMonth) {
        for (let elem of this.sortedUsersByDay) {
          if (item.birthday_contact === elem.birthday_contact) {
            this.sortedUsersTotal.push(item)
          }
        }
      }
    },
    sortedUsersByDay(){
      this.sortedUsersTotal = [];
      for (let item of this.sortedUsersByDay) {
        for (let elem of this.sortedUsersByMonth) {
          if (item.birthday_contact === elem.birthday_contact) {
            this.sortedUsersTotal.push(item)
          }
        }
      }
    },
  },
  computed: {
    filteredUsers() {
      if (this.sortedUsersTotal.length) {        
        return this.sortedUsersTotal
      } else {
        return this.sortedUsersTotal
      }
    },    
  },
  methods: {
    sortByMonth(option) {       
      this.sortedUsersByMonth = [];
      let vm = this;      
      this.users_data.map(function(item) {        
        let date = new Date(item.birthday_contact);
        let userMonth = (date.getMonth()+1);
        if(userMonth === option.value) {          
          vm.sortedUsersByMonth.push(item)          
        }
        if(option.value === 0) {       
          vm.sortedUsersByMonth.push(item)          
        }
      })
      this.selectedMonth = option.name;
    },
    sortByDay(option) {       
      this.sortedUsersByDay = [];
      let vm = this;      
      this.users_data.map(function(item) {        
        let date = new Date(item.birthday_contact);
        let userDay = (date.getDate());
        if(userDay === option.value) {          
          vm.sortedUsersByDay.push(item)          
        }
        if(option.value === 0) {       
          vm.sortedUsersByDay.push(item)          
        }
      })
      this.selectedDay = option.name;
    },    
  },
  mounted() {
    
  },
}
</script>

<style lang="scss">
  .v-table {
    max-width: 900px;
    margin: 0 auto;

    .selects-wrapper {
      display: flex;
      flex-direction: row;
      justify-content: flex-start;
    }

    &__header {
      display: flex;
      flex-direction: row;
      justify-content: space-between;
      align-items: center; 
      background-color: #eeeeee;     
    }

    .body__row {
      border-bottom: 1px solid #dddddd;
    }
    
    &__data {
      flex-basis: 16%;
      text-align: left;
      padding: 8px 16px;
    }
    .err-message {
      color: #aeaeae;
    }
  }

</style>