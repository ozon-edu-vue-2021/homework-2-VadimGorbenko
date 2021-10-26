<template>
  <div :class="['files-item', `files-item_type_${item.type}`, {'files-item_opened': isDirectory && itemOpened}]" @click.stop="showPath">
    <div class="files-item__image"></div>
    <template v-if="isDirectory">
      <button type="button" class="files-item__item" @click="toggleDirectory"><span class="v-h">Каталог: </span>{{ item.name }}</button>
      <transition name="fade">
        <files-three v-if="itemOpened" :data="item.contents" :path="pathToItem"/>
      </transition>
    </template>
    <a v-else-if="isLink" :href="item.target" class="files-item__item" @click.prevent>{{ item.name }}</a>
    <button v-else class="files-item__item" tabindex="0"><span class="v-h">Файл: </span>{{ item.name }}</button>
  </div>
</template>

<script>
export default {
  components: { 
    FilesThree: () => import('./FilesThree.vue')
  },
  name: 'FilesItem',
  inject: ['showSelectedItemPath'],
  props: {
    item: {
      type: Object,
      required: true,
    },
    path: {
      type: String,
      default: '',
    }
  },
  data() {
    return {
      itemOpened: false
    }
  },
  computed: {
    isDirectory() {
      return this.item.type === 'directory'
    },
    isLink() {
      return this.item.type === 'link'
    },
    pathToItem() {
      return this.path === this.item.name ? this.path : `${this.path}/${this.item.name}`;
    }
  },
  methods: {
    toggleDirectory() {
      this.itemOpened = !this.itemOpened
    },
    showPath() {
      this.showSelectedItemPath(this.pathToItem)
    }
  }
}
</script>

<style>
.fade-enter-active, .fade-leave-active {
  transition: opacity .5s;
}
.fade-enter, .fade-leave-to{
  opacity: 0;
}

.files-item {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
}

.files-item:focus-within {
    outline: 1px solid gray;
}


.files-item .files-three {
  width: 100%;
}

.files-item__image {
  display: inline-block;
  margin-right: 4px;
  width: 24px;
  height: 24px;
  background-size: cover;
  background-repeat: no-repeat;
}

.files-item_type_directory > .files-item__image {
  background-image: url('../../assets/folder.png');
}

.files-item_type_directory.files-item_opened > .files-item__image {
  background-image: url('../../assets/folder_opened.png');
}

.files-item_type_file > .files-item__image {
  background-image: url('../../assets/file.png');
}

.files-item_type_link > .files-item__image {
  background-image: url('../../assets/link.png');
}

.files-item__item {
  border: none;
  background-color: transparent;
  color: inherit;
  font-size: 1em;
  padding: 2px;
}
</style>