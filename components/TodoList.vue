<template>
 <div class="columns">
   <button @click="changedAtoB">changedAtoB</button>
   <div class="column">{{ aList }}</div>
   <div class="column">{{ bList }}</div>
 </div>
</template>

<script lang="ts">
import {
  defineComponent,
  reactive,
  ref,
  SetupContext,
  onMounted,
  watch,
  computed
  } from '@vue/composition-api'
interface Task {
  id: number
  name: string
  ab: 'a' | 'b'
}
export default defineComponent({

  setup (_props, { emit }: SetupContext) {
    let
    const count = ref<number>(0)
    const name = ref<string>('hello')
    const list = ref<Task[]>([])

    const item = reactive<Task>({
      id: 1,
      name: 'hello 1',
      ab: 'a'
    })
    list.value.push(item,
    reactive<Task>({
      id: 2,
      name: 'hello 2',
      ab: 'a'
    }),
    reactive<Task>({
      id: 3,
      name: 'hello 3',
      ab: 'b'
    }),
    reactive<Task>({
      id: 4,
      name: 'hello 4',
      ab: 'b'
    })
    )

    function increment () {
      count.value++
    }

    function changeItem (newItem: Task) {
      for (const key in newItem) {
        const element = newItem[key as keyof Task]
        item[key as keyof Task] = element as never
      }
    }

    function changedAtoB () {
      item.ab = 'b'
    }

    const aList = computed(() => list.value.filter((x) => x.ab === 'a'))
    const bList = computed(() => list.value.filter((x) => x.ab === 'b'))

    const nameCount = computed(() => {
      return `${name.value}-${count.value}`
    })

    function changeName () {
      name.value = 'changed'
    }

    onMounted(() => {
      item.name = 'on mounted'
    })

    return {
      count,
      name,
      list,
      item,
      increment,
      changeItem,
      changeName,
      nameCount,
      aList,
      bList,
      changedAtoB,
    }
  }
})
</script>

<style>

</style>
