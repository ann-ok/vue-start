<template>
  <div id="app">
    <Header msg="Добро пожаловать"/>

    <div>
      <h3>Добавление элемента:</h3>
      <!--Новый элемент получает id, равный количеству элементов,
       + 1 так как количество увеличится при добавлении-->
      <AddItem @add-item="addItem(items.length + 1, $event)"/>
    </div>

    <div>
      <h3>Сортировка:</h3>
      <select v-model="sort" @change="changeSort">
        <option v-for="sortType in sortTypes"
                :value="sortType.name"
                :key="sortType.name">
          {{sortType.text}}
        </option>
      </select>
    </div>

    <div>
      <h3>Список:</h3>
      <template v-if="items.length">
        <ul>
          <Item v-for="(item, index) in items"
                :item="item"
                :key="item.id"
                @delete-item="deleteItem(index, $event)"
                @edit-item="editItem(index, $event)"
          />
        </ul>
        <span>количество элементов: {{items.length}}</span>
      </template>
      <span v-else>Элементов нет</span>
    </div>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Item from "@/components/Item";
import AddItem from "@/components/AddItem";

export default {
  name: 'App',
  components: {
    AddItem,
    Item,
    Header
  },
  data() {
    return {
      items: [{id: 1, text: 'Первый'},
        {id: 2, text: 'Второй'},
        {id: 3, text: 'Третий'}],
      sort: 'id-asc',
      sortTypes: [{name: 'id-asc', text: 'По возрастанию номера'},
        {name: 'id-desc', text: 'По убыванию номера'},
        {name: 'text-asc', text: 'По алфавиту'},
        {name: 'text-desc', text: 'По алфавиту в обратном порядке'}]
    }
  },
  methods: {
    addItem(id, text) {
      this.items.push({id: id, text: text});
      this.changeSort();
    },
    editItem(index, newItem) {
      this.items.splice(index, 1, newItem);
      this.changeSort();
    },
    deleteItem(index, id) {
      this.items.splice(index, 1);
      for (let i = 0; i < this.items.length; i++) {
        if (this.items[i]['id'] >= id) {
          this.items[i]['id']--;
        }
      }
    },
    changeSort() {
      const sort  = this.sort;
      this.items.sort(function (a, b) {
        const typeSort = sort.includes('id') ? 'id' : 'text';
        console.log();
        const aVal = a[typeSort].toString();
        const bVal = b[typeSort].toString();
        return sort.includes('asc')
                ? aVal.localeCompare(bVal)
                : bVal.localeCompare(aVal) ;
      });
    }
  }
}
</script>

<style>
  ul {
    list-style-type: none;
    padding-left: 10px;
  }
</style>
