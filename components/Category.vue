<template>
  <div class="row">
    <div v-for="category in categories" :key="category.id" class="col-md-4">
      <div class="image-container">
        <NLink :to="'/Account/' + category.name">
          <img
            :src="`../${category.imageUrl}`"
            class="img-fluid"
            alt="Responsive image"
          />
          <div class="centered">
            <p>{{ category.name }}</p>
          </div>
        </NLink>
      </div>
    </div>
  </div>
</template>

<script>
import categories from '@/data/categories.json'
export default {
  props: {
    name: {
      type: String,
      default: ''
    },
    imageUrl: {
      type: String,
      default: ''
    }
  },
  data() {
    return {
      categories
    }
  }
}
</script>
<style scoped>
.image-container {
  width: 70%;
  margin-top: 8%;
  margin-left: 5%;
  box-shadow: 0 0 5px;
  transition: box-shadow 0.3s;
}
.image-container:hover {
  box-shadow: 0 0 14px;
}
.centered {
  position: absolute;
  top: 58%;
  left: 35%;
  color: white;
  font-size: 1.7em;
  font-weight: bold;
  transform: translate(-30%, -40%);
}
p {
  text-shadow: 2px 2px 5px black;
}
</style>
