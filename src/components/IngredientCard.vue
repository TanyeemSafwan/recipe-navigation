<script setup>
import { computed, ref } from 'vue'

const toggleAmount = ref(true)
const props = defineProps(['items', 'name'])
const chosenProductsCount = computed(() => props.items.filter((item) => item.active).length)
// const items = ref([
//   {
//     id: 1,
//     name: 'egg',
//     active: false
//   },
//   {
//     id: 2,
//     name: 'butter',
//     active: false
//   },
//   {
//     id: 3,
//     name: 'garlic',
//     active: false
//   },
//   {
//     id: 4,
//     name: 'onion',
//     active: false
//   },
//   {
//     id: 5,
//     name: 'sugar',
//     active: false
//   },
//   {
//     id: 6,
//     name: 'milk',
//     active: false
//   },
//   {
//     id: 7,
//     name: 'flour',
//     active: false
//   },
//   {
//     id: 8,
//     name: 'olive oil',
//     active: false
//   },
//   {
//     id: 9,
//     name: 'garlic powder',
//     active: false
//   },
//   {
//     id: 10,
//     name: 'white rice',
//     active: false
//   },
//   {
//     id: 11,
//     name: 'cinnamon',
//     active: false
//   },
//   {
//     id: 12,
//     name: 'ketchup',
//     active: false
//   },
//   {
//     id: 13,
//     name: 'soy sauce',
//     active: false
//   },
//   {
//     id: 14,
//     name: 'mayonnaise',
//     active: false
//   },
//   {
//     id: 15,
//     name: 'vegetable oil',
//     active: false
//   },
//   {
//     id: 16,
//     name: 'bread',
//     active: false
//   },
//   {
//     id: 17,
//     name: 'baking powder',
//     active: false
//   },
//   {
//     id: 18,
//     name: 'brown sugar',
//     active: false
//   },
//   {
//     id: 19,
//     name: 'oregano',
//     active: false
//   },
//   {
//     id: 20,
//     name: 'potato',
//     active: false
//   }
// ]);
</script>
<template>
  <div class="card-container">
    <div class="header-container">
      <div style="width: 30%">
        <img
          height="100px"
          width="100px"
          src="../assets/images/pastry-essentials.png"
          alt="pantry_es"
        />
      </div>
      <div style="width: 65%">
        <h3 class="header-design">
          {{ props.name.split('_').join(' ').toUpperCase() }}
        </h3>
        <p>{{ `${chosenProductsCount}/${props.items.length}` }} Ingredients</p>
      </div>
      <div style="width: inherit; margin-left: auto">
        <img
          v-if="toggleAmount"
          @click="toggleAmount = !toggleAmount"
          src="../assets/images/dropdown.png"
          height="15px"
          width="15px"
        />
        <img
          v-if="!toggleAmount"
          @click="toggleAmount = !toggleAmount"
          src="../assets/images/arrow-up.png"
          height="15px"
          width="15px"
        />
      </div>
    </div>
    <hr style="margin-bottom: 20px" />
    <div>
      <button
        v-if="!toggleAmount"
        v-for="item of props.items"
        :key="item.id"
        class="item-button"
        :class="item.active ? 'active-button' : ''"
        @click="$emit('toggleActive', item.id, props.name)"
      >
        {{ item.name }}
      </button>
      <button
        v-if="toggleAmount"
        v-for="index in 10"
        :key="index"
        class="item-button"
        :class="props.items[index].active ? 'active-button' : ''"
        @click="$emit('toggleActive', props.items[index].id, props.name)"
      >
        {{ props.items[index].name }}
      </button>
      <button class="item-button" @click="toggleAmount = !toggleAmount">
        {{ toggleAmount ? `+${items.length - 10} more` : `Show less` }}
      </button>
    </div>
  </div>
</template>

<style scoped>
.card-container {
  width: 100%;
  border-radius: 10px;
  padding: 15px;
  max-width: 400px;
  box-shadow:
    0 4px 8px 0 rgba(0, 0, 0, 0.2),
    0 6px 20px 0 rgba(0, 0, 0, 0.19);
}
.header-design {
  font: 1.2em sans-serif;
  margin-bottom: 30px;
}
.header-container {
  display: flex;
}
.item-button {
  background-color: #f0f2f4;
  border: none;
  cursor: pointer;
  border-radius: 10px;
  padding: 15px 12px;
  margin-right: 10px;
  margin-bottom: 10px;
}
.active-button {
  background: #95c762;
}
</style>
