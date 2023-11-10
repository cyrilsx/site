---
title: "Define props with composition API"
date: 2023-11-21T15:28:25+02:00
tags: [frontend, dev, vue3] 
---
I didn't find it easily at first but I'm writing a note about this. How to pass properties to a Vue Component using the Composition API ?
This code is a part of the online course from [vueschool.io](https://vueschool.io/). 

Let's start with the client component.
```
<script setup>
import ThreadList from '@/components/ThreadList.vue'
import { reactive } from 'vue'
import sourceData from '@/data.json'

const threads = reactive(sourceData.threads)
</script>

<template>
  <ThreadList :threads="threads" />
</template>
```

Now inside the component `ThreadList`, we need to declare and access the properties (also called props in Vue3):

```
/** Macro to define props */
const props = defineProps({
  threads: {
    type: Array,
    required: true
  }
})

const threads = props.threads
```

As you can see, a special function `defineProps` which takes an object with the _props_ definition have to be declared. It just serves at the compile phase.
The return variable can be use to access _props_.

That's all for today.
Have a great weekend.
