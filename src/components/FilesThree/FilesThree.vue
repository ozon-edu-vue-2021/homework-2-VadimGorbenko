<template>
  <ul class="files-three">
    <li v-for="(item, idx) in items" :key="idx">
      <files-item :item="item" :path="getPath(item)" />
    </li>
  </ul>
</template>

<script>
/**
 * TODO:
 * DONE 1. Иконки для разных типов файлов; (В том числе другую для открытой папки)
 * DONE 2. Выделение элементов по клику на них
 * 3. Сэмулировать проводник, типа окошко, внутри которого это всё происходит.
 * DONE 4. Навигацию с клавиатуры
 * DONE 5. Вывод полного пути до текущего выделенного файла
 * 6. Реализовать по WCAG three
 * 7. Добавить aria-live по факту выделения элемента - озвучивать полный путь
 * DONE 8. Поработать с доступностью: например, добавить скрытое слово "каталог" для всех папок и слово "файл" для файлов. Ссылку итак озвучит.
 */
export default {
  name: 'FilesThree',
  components: {
    FilesItem: () => import('./FilesItem.vue')
  },
  props: {
    data: {
      type: [Object, Array],
      required: true,
    },
    path: {
      type: String,
      default: ''
    }
  },
  computed: {
    items() {
      return Array.isArray(this.data) ? this.data : [this.data]
    },
  },
  methods: {
    getPath(item) {
      return this.path || item.name;
    }
  }
}
</script>

<style>
.files-three {
  margin: 0;
  padding: 5px 10px 5px 24px;
  text-align: left;
  list-style-type: none;
}

.files-three li {
    margin: 4px 0px;
}
</style>