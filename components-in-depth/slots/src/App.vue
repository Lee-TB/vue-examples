<script setup>
import SubmitButton from './SubmitButton.vue';
import BaseLayout from './BaseLayout.vue';
import SlotProps from './SlotProps.vue';
import FancyList from './FancyList.vue';
import MouseTraker from './MouseTraker.vue';
</script>

<template>
  <h2>Fallback content</h2>
  <div>
    <SubmitButton />
    <SubmitButton>Save</SubmitButton>
  </div>
  <h2>Named slots</h2>
  <BaseLayout>
    <template v-slot:header>
      <p>Header content</p>
    </template>

    <!-- explicit default slot -->
    <!-- <template #default>
      <p>default content</p>
    </template> -->

    <!-- implicit default slot -->
    <p>implicit default slot</p>

    <template #footer>
      <p>Footer content</p>
    </template>
  </BaseLayout>

  <h2>Slot props</h2>
  <SlotProps v-slot="slotProps">
    {{ slotProps.text }} {{ slotProps.count }}
  </SlotProps>

  <h2>FancyList exmaple</h2>
  <FancyList :api-url="url" :per-page="10">
    <template #item="{ body, username, likes }">
      <div class="item">
        <p>{{ body }}</p>
        <p>by {{ username }} | {{ likes }} likes</p>
      </div>
    </template>
  </FancyList>

  <h2>Renderless components (Mouse Tracker)</h2>
  <MouseTraker v-slot="{ x, y }"> Position: ({{ x }}, {{ y }}) </MouseTraker>
</template>
