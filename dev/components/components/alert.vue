<template>
  <div class="layout-padding">
    <q-btn color="primary" class="fixed" style="right: 18px; bottom: 18px" @click="reset">Reset</q-btn>

    <q-btn style="margin-bottom: 25px" color="primary" @click="alertAsMethod">Show Alert as Method</q-btn>

    <q-btn style="margin-bottom: 25px" color="primary" @click="alertAsComponent">Show Alert as Component</q-btn>

    <q-transition
      enter="bounceInLeft"
      leave="bounceOutRight"
      appear
    >
      <q-alert
        color="brown"
        ref="brownAlert"
        style="margin-bottom: 1.5rem"
        v-show="visible1"
        v-model="visible1"
        dismissible
      >
        <q-icon name="cloud" slot="left" />
        Lorem ipsum dolor sit amet.
      </q-alert>
    </q-transition>

    <q-alert
      type="negative"
      ref="destroyableAlert"
      dismissible
      @dismiss="$refs.destroyableAlert.destroy()"
      style="margin-bottom: 1.5rem"
      :buttons="[{label: 'Snooze', handler () {}}]"
    >
      Dest. Lorem ipsum dolor sit amet.
    </q-alert>

    <q-transition
      v-for="type in ['positive', 'info', 'negative', 'warning']"
      :key="type"
      enter="bounceInLeft"
      leave="bounceOutRight"
      appear
    >
      <q-alert
        :color="type"
        v-show="visible"
        v-model="visible"
        ref="alert"
        dismissible
        style="margin-bottom: 1.5rem"
      >
        Lorem ipsum dolor sit amet.
      </q-alert>
    </q-transition>

    <!--
    <q-alert style="margin-bottom: 1.5rem">
      <q-spinner color="white" :size="24" slot="left" />
      Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
    </q-alert>
    -->

    <q-alert
      v-for="type in ['positive', 'info', 'negative', 'warning']"
      :key="type"
      :color="type"
      ref="alert"
      style="margin-bottom: 1.5rem"
    >
      Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
    </q-alert>

    <div v-if="showGreenAlert">
      <q-transition
        enter="bounceInRight"
        leave="bounceOutRight"
        appear
        @after-leave="greenAlertDissmissed"
      >
        <q-alert
          color="green"
          ref="greenAlert"
          style="margin-bottom: 1.5rem"
          dismissible
          v-show="greenAlertVisible"
          v-model="greenAlertVisible"
          position="top-right"
        >
          <q-icon name="thumb_up" slot="left" />
          {{ greenAlertText }}
        </q-alert>
      </q-transition>
    </div>

  </div>
</template>

<script>
import { Alert } from 'quasar'
import 'animations/bounceInLeft.css'
import 'animations/bounceOutRight.css'
import 'animations/zoomIn.css'
import 'animations/zoomOut.css'

Alert.create({html: 'Warning, warning Will Robinson!'})

export default {

  data () {
    return {
      visible: true,
      visible1: true,
      showGreenAlert: false,
      greenAlertVisible: true,
      greenAlertText: 'Excellent!'
    }
  },
  methods: {
    alertAsMethod () {
      Alert.create({
        enter: 'zoomIn',
        leave: 'zoomOut',
        color: 'blue',
        icon: 'wifi',
        html: 'A text with your alert\'s awesome message',
        position: 'top',
        buttons: [
          {
            label: 'Snooze',
            handler () {
              console.log('acting')
            }
          },
          {
            label: 'Abort',
            handler () {
              console.log('aborting')
            }
          }
        ]
      })
      // alert.dismiss()
    },
    reset () {
      this.$refs.alert.forEach(alert => {
        alert.show()
      })
    },
    alertAsComponent () {
      this.showGreenAlert = true
    },
    greenAlertDissmissed () {
      this.showGreenAlert = false
      this.greenAlertVisible = true
    }
  }
}
</script>
