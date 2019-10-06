<template>
  <div>
    <div class="page-title">
      <h3>Категории</h3>
    </div>
    <section>
      <div class="row">
        <CategoryCreate @created="addNewCategory"/>
        <CategoryEdit />
      </div>
    </section>
  </div>
</template>

<script>
import CategoryCreate from '@/components/CategoryCreate'
import CategoryEdit from '@/components/CategoryEdit'

export default {
  data() {
    return {
      categories: []
    }
  },
  components: {
    CategoryCreate, CategoryEdit
  },
  methods: {
    addNewCategory(categories) {
      this.categories.push(categories)
      console.log(this.categories)
    }
  }
}
</script>
