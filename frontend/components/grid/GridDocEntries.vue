<template>
  <div class="grid w-full grid-cols-1 gap-5 md:gap-8 md:grid-cols-2 h-fit">
    <CardDocsEntry
      v-for="card in cards"
      :url="route.path.replace(/\/$/, '') + '/' + card.url"
      :imgURL="card.imgURL"
      :imgDimensions="card.imgDimensions"
      :imgAltText="card.imgAltText"
      :title="card.title"
      :description="card.description"
    />
  </div>
</template>

<script setup lang="ts">
import type { CardDocsEntry } from "../../types/card-docs-entry";

defineProps<{
  cards?: CardDocsEntry[];
}>();

var route = useRoute();
</script>
