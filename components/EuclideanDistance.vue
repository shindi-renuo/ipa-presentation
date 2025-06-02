<template>
  <div>
    <h3 class="text-lg font-bold mb-2">Beispiel: Euklidische Distanz</h3>
    <table class="table-auto border-collapse w-full">
      <thead>
        <tr>
          <th class="border border-gray-300 px-2 py-1">Vektor</th>
          <th class="border border-gray-300 px-2 py-1">Werte</th>
          <th class="border border-gray-300 px-2 py-1">Distanz</th>
          <th class="border border-gray-300 px-2 py-1">Visualisierung</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in sortedVectors" :key="index">
          <td class="border border-gray-300 px-2 py-1">V{{ index }}</td>
          <td class="border border-gray-300 px-2 py-1">{{ JSON.stringify(item.vector) }}</td>
          <td class="border border-gray-300 px-2 py-1">{{ item.distance.toFixed(2) }}</td>
          <td class="border border-gray-300 px-2 py-1">
            <div class="h-2 bg-blue-500" :style="{ width: `${(item.distance / maxDistance) * 100}%` }"></div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup>
import { computed } from 'vue'

const referenceVector = [2, 7, -4]
const vectors = [
  [1, 6, -3],
  [-1, 3, 2],
  [4, 9, -6],
  [0, 0, 0],
  [10, -2, 5],
  [2, 7, -4]
]

// Calculate euclidean distance between two vectors
const calculateDistance = (vec1, vec2) => {
  let sum = 0
  for (let i = 0; i < vec1.length; i++) {
    sum += (vec1[i] - vec2[i]) ** 2
  }
  return Math.sqrt(sum)
}

// Calculate distances and sort by similarity
const sortedVectors = computed(() => {
  const results = vectors.map(vector => ({
    vector,
    distance: calculateDistance(referenceVector, vector)
  }))

  return results.sort((a, b) => a.distance - b.distance)
})

const maxDistance = computed(() => {
  return Math.max(...sortedVectors.value.map(item => item.distance))
})
</script>
