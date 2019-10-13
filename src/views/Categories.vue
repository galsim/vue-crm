<template>
  <div>
    <div class="page-title">
      <h3>Категории</h3>
    </div>
    <section>
      <Loader v-if="loading"/>
      <div v-else class="row">
        <CategoryCreate @created="addNewCategory"/>
        <CategoryEdit 
          :key="categories.length + updateCount" 
          @updated="updateCategories" 
          v-if="categories.length" 
          :categories="categories"/>
        <p v-else class="center">Категорий нет</p>
      </div>
    </section>
  </div>
</template>

<script>
import CategoryCreate from '@/components/CategoryCreate'
import CategoryEdit from '@/components/CategoryEdit'

export default {
  metaInfo() {
    return {
      title: this.$title('Menu_Categories')
    }
  },
  data() {
    return {
      categories: [],
      loading: true,
      updateCount: 0
    }
  },
  components: {
    CategoryCreate, CategoryEdit
  },
  async mounted() {
    this.categories = await this.$store.dispatch('fetchCategories')
    this.loading = false
  },
  methods: {
    addNewCategory(categories) {
      this.categories.push(categories)
    },
    updateCategories(category) {
      const idx = this.categories.findIndex(c => c.id === category.id)
      this.categories[idx].title = category.title
      this.categories[idx].limit = category.limit
      this.updateCount += 1
    }
  }
}
</script>
