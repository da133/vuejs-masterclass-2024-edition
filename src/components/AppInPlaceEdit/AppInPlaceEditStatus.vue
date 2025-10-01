<script setup lang='ts'>
  const value = defineModel<'in-progress' | 'completed'>()

  const emit = defineEmits(['commit'])

  const {readonly = false} = defineProps<{
    readonly?: boolean
  }>()

  const toggleValue = () => {
    if (readonly) return

    value.value = value.value === 'completed' ? 'in-progress' : 'completed'
    emit('commit')
  }
</script>

<template>
  <div class="text-2x1 cursor-pointer flex items-center" @click="toggleValue">
    <Transition name="scale" mode="out-in">
      <iconify-icon v-if="value === 'completed'" icon="lucide:circle-check" class="text-green-500 text-xl" />
      <iconify-icon v-else icon="lucide:circle-dot" class="text-gray-500 text-xl" />
    </Transition>
  </div>
</template>
