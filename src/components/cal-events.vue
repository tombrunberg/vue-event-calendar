<template>
  <div class="events-wrapper" :style="bgColor">
    <h2 class="date">
      {{dayEventsTitle}}
    </h2>
    <div class="cal-events">
      <slot>

        <div class='rolewrap' v-if="hasRoles('pilot', events)">
          <h2>Pilots </h2>
          <div class="event-item">
            <div v-for="(event, index) in sortOut('pilot',events)" class="">
              <cal-event-item :event="event" :index="index" :locale="locale"></cal-event-item>
            </div>
          </div>
        </div>

        <div class='rolewrap' v-if="hasRoles('licensed', events)">
          <h2>Licensed</h2>
          <div class="event-item">
            <div v-for="(event, index) in sortOut('licensed',events)" class="">
              <cal-event-item :event="event" :index="index" :locale="locale"></cal-event-item>
            </div>
          </div>
        </div>

        <div class='rolewrap' v-if="hasRoles('student', events)">
          <h2>Students</h2>
          <div class="event-item">
            <div v-for="(event, index) in sortOut('student',events)" class="">
              <cal-event-item :event="event" :index="index" :locale="locale"></cal-event-item>
            </div>
          </div>
        </div>

      </slot>
    </div>
  </div>
</template>

<script>
import i18n from '../i18n.js'
import { dateTimeFormatter } from '../tools.js'
import calEventItem from './cal-event-item.vue'
export default {
  name: 'cal-events',
  data () {
    return {
      i18n
    }
  },
  components: {
    'cal-event-item': calEventItem
  },
  props: {
    dayEvents: {
      type: Object,
      required: true
    },
    locale: {
      type: String,
      required: true
    }
  },
  computed: {
    dayEventsTitle () {
      if (this.dayEvents.date !== 'all') {
        let tempDate
        if (this.dayEvents.events.length !== 0) {
          tempDate = Date.parse(new Date(this.dayEvents.events[0].date))
          return dateTimeFormatter(tempDate, i18n[this.locale].fullFormat)
        } else {
          tempDate = dateTimeFormatter(Date.parse(new Date(this.dayEvents.date)), i18n[this.locale].fullFormat)
          return `${tempDate} ${i18n[this.locale].notHaveEvents}`
        }
      } else {
        return i18n[this.locale].dayEventsTitle
      }
    },
    events () {
      return this.dayEvents.events
    },
    bgColor () {
      return {backgroundColor: this.color}
    }
  },
  methods: {
    dateTimeFormatter,
    hasRoles (role,events) {
      let count = 0

      events.map(function(elem, index){
        console.log( elem.role )
        console.log( ' vs ' + role )
        if( elem.role == role ) {
          count++
        }
      })
      console.log(count)
      return count
    },
    sortOut (role, events) {

      let tempArr = [];

      events.map(function(elem, index){
        if( elem.role == role )
          tempArr.push(elem)
      })

      return tempArr
    }
  }
}
</script>