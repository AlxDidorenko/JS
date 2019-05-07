<template>
  <v-data-table
    :headers="headers"
    :items="students"
    class="elevation-1"
  >
    <template v-slot:items="props">
      <td>{{ props.item.name }}</td>
      <td class="text-xs-right">{{ props.item.surname }}</td>
      <td class="text-xs-right">{{ props.item.date_birth }}</td>
      <td class="text-xs-right">{{ props.item.n_group }}</td>
      <td class="text-xs-right">{{ props.item.score }}</td>
      <td class="text-xs-right">{{ props.item.city }}</td>
      <td class="text-xs-right">{{ props.item.address }}</td>
    </template>
  </v-data-table>
</template>

<script>
import axios from 'axios'

  export default {
    data () {
      return {
        headers: [
          {
            text: 'Имя',
            align: 'left',
            sortable: false,
            value: 'name'
          },
          { text: 'Фамилия', value: 'surname' },
          { text: 'Дата рождения', value: 'date_birth' },
          { text: 'Номер группы', value: 'n_group' },
          { text: 'Средний балл', value: 'score' },
          { text: 'Город', value: 'city' },
          { text: 'Адрес', value: 'address' }
        ],
        students: []    
      }
    },
    created() {
      axios
      .get('http://localhost:8081/api/students')
      .then(response => {
        console.log(response)
        this.students=response.data
      })
      .catch(error => {
        console.log(error)
      })
    }
    // запрос к api, чтобы получить данные
  }
</script>