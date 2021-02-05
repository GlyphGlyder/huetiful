<!-- A section for showing off a specific mode or thing Huetiful can do. -->
<template>

  <div class="context" :style="{'background-color': `rgb(${red}, ${green}, ${blue})`}">

    <div class="target"/>

    <slot></slot>

  </div>

</template>

<script>
export default {
  name: "DemoSection",
  props: ['red', 'green', 'blue']
}
</script>
