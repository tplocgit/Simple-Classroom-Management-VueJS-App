<template>
  <div class="item">
    <p>
      Name: {{ item.name }}
    </p>
    <p>
      Topic: {{ item.theme }}
    </p>
    <p>
      Section: {{ item.part }}
    </p>
  </div>
</template>

<script>
export default {
  name: 'Item',
  props: {
    item: Object
  }
}
</script>
