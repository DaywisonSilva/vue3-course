<template>
  <div>
    <h1>Lifecycle Hooks</h1>

  </div>
</template>

<script>
import { onMounted } from '@vue/runtime-core'
export default {
  setup() {
    onMounted(() => {
      console.log("mo ntado com onMounted")
    })
  }
}


// export default {
//   mounted() {
//     console.log('Foi montado options API')
//   }
// }
// </script>