<template>
  <div class="wrapper">
    <p>
      <span><b>{{event.title}}</b></span>
    </p>
    <p>{{event.desc}}</p>
  </div>
</template>
<script>
import i18n from '../i18n.js'
import { dateTimeFormatter } from '../tools.js'
export default {
  data () {
    return {
      i18n
    }
  },
  props: {
    event: {
      type: Object,
      required: true
    },
    index: {
      type: Number,
      required: true
    },
    locale: {
      type: String,
      required: true
    },
    role: {
      type: String,
      required: false,
    }
  },
  methods: {
    dateTimeFormatter
  }
}

</script>