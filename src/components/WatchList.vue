<script setup>
defineProps({
  items: {
    type: Array,
    default: () => [],
  },
})

const emit = defineEmits(['remove'])
</script>

<template>
  <aside
    class="rounded-3xl border border-purple-500/50 bg-purple-950/60 p-5 shadow-xl shadow-purple-950/30 backdrop-blur-sm"
  >
    <div class="mb-4 flex items-center justify-between">
      <h2 class="text-xl font-bold text-white">Watchlist</h2>
      <span class="rounded-full bg-purple-800 px-3 py-1 text-xs font-semibold text-purple-100">{{
        items.length
      }}</span>
    </div>

    <p
      v-if="!items.length"
      class="rounded-2xl border border-purple-500/50 bg-purple-900/60 p-4 text-sm text-purple-200"
    >
      No picks saved yet. Spin and add an anime to build your watchlist.
    </p>

    <ul
      v-else
      class="space-y-3"
    >
      <li
        v-for="item in items"
        :key="item.mal_id"
        class="rounded-2xl border border-purple-500/50 bg-purple-900/60 p-3"
      >
        <div class="flex gap-3">
          <img
            v-if="item.image"
            :src="item.image"
            :alt="item.title"
            class="h-20 w-14 rounded-md object-cover"
            loading="lazy"
          />
          <div
            v-else
            class="flex h-20 w-14 items-center justify-center rounded-md bg-purple-800 text-xs text-purple-200"
          >
            N/A
          </div>

          <div class="min-w-0 flex-1">
            <h3 class="truncate text-sm font-semibold text-white">{{ item.title }}</h3>
            <p class="mt-1 text-xs text-purple-200">
              ⭐ {{ item.score ?? 'N/A' }} · Ep {{ item.episodes ?? '?' }} ·
              {{ item.rating || 'Unrated' }}
            </p>
            <div class="mt-3 flex flex-wrap gap-2">
              <a
                :href="item.url"
                target="_blank"
                rel="noopener noreferrer"
                class="text-xs font-semibold text-pink-300 hover:underline"
              >
                MAL Link
              </a>
              <button
                type="button"
                class="text-xs font-semibold text-rose-300 hover:underline"
                @click="emit('remove', item.mal_id)"
              >
                Remove
              </button>
            </div>
          </div>
        </div>
      </li>
    </ul>
  </aside>
</template>
