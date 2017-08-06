<template>
    <label :class="classMerged">
        <input type="checkbox"
               class="Qswitch-input"
               v-model="isChecked"
               :name="name"
               :value="value"
               :checked="isChecked"
               :disabled="disabled">
        <span class="Qswitch-label" :data-on="text_on" :data-off="text_off" :class="icon"></span>
        <span class="Qswitch-handle"></span>
    </label>
</template>
<script>
  'use strict'
  export default {
    name: 'Qswitch',
    /*
    * 默认情况下，一个组件的v-model会使用value属性和input事件，但诸如radio、checkbox之类的输入类型
    * 可能把value属性用作了别的目的。model选项可以回避这样的冲突：
     */
    model: {
      prop: 'checked',
      event: 'change'
    },
    watch: {
      isChecked (val) {
        this.$emit('change', Boolean(val))
      }
    },
    data () {
      return {
        isChecked: this.checked
      }
    },
    props: {
      name: String,
      value: String,
      checked: Boolean,
      disabled: Boolean,
      type: {
        type: String, // 'default' 'text' 'con' '3d'
        required: false,
        default: 'default'
      },
      size: {
        type: String, // 'mini' 'small' 'default' 'big'
        required: false,
        default: 'default'
      },
      icon: {
        type: String, // 'happy' 'lock' 'check' 'check2' 'check3' 'check4'
        required: false,
        default: ''
      },
      color: {
        type: String,
        required: false,
        default: 'blue'
      },
      pill: Boolean,
      outline: Boolean,
      alt: Boolean,
      text_off: String,
      text_on: String
    },
    computed: {
      classMerged: function () {
        let { type, size, color, pill, outline, alt } = this
        return [
          'Qswitch',
          this.__getSize(size),
          this.__getType(type),
          pill ? 'Qswitch-pill' : '',
          this.__getColor(color) + (alt ? '-outline-alt' : (outline ? '-outline' : ''))
        ]
      }
    },
    methods: {
      __getSize: function (size = 'default') {
        let allowedSizes = {'mini': 'Qswitch-xs', 'small': 'Qswitch-sm', 'default': '', 'big': 'Qswitch-lg'}
        return allowedSizes[size]
      },
      __getType: function (type = 'default') {
        let allowedTypes = {'default': 'Qswitch-default', 'text': 'Qswitch-text', 'icon': 'Qswitch-icon', '3d': 'Qswitch-ddd'}
        return allowedTypes[type]
      },
      __getIcon: function (icon = '') {
        let allowedIcons = {'happy': 'happy', 'lock': 'lock', 'check': 'check', 'check2': 'check2', 'check3': 'check3', 'check4': 'check4'}
        return allowedIcons[icon]
      },
      __getColor: function (color = 'blue') {
        let allowedColors = {
          'black': 'Qswitch-black',
          'aqua': 'Qswitch-aqua',
          'blue': 'Qswitch-blue',
          'fuchsia': 'Qswitch-fuchsia',
          'green': 'Qswitch-green',
          'lime': 'Qswitch-lime',
          'maroon': 'Qswitch-maroon',
          'navy': 'Qswitch-navy',
          'olive': 'Qswitch-olive',
          'orange': 'Qswitch-orange',
          'purple': 'Qswitch-purple',
          'red': 'Qswitch-red',
          'silver': 'Qswitch-silver',
          'gray': 'Qswitch-gray',
          'teal': 'Qswitch-teal',
          'yellow': 'Qswitch-yellow'
        }
        return allowedColors[color]
      }
    }
  }
</script>
<style lang="sass" scoped>@import "../scss/Qswitch.scss"</style>