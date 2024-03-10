<template>
  <div class="font-awesome-search">
    <el-input v-model="search" placeholder="Search icons…"></el-input>
    <el-button v-for="icon in matchedIcons" :class="['fa', `fa-${icon.id}`]" :title="icon.name"
      :key="icon.id" @click="click(icon)">
    </el-button>
  </div>
</template>

<script>
import icons from '../icons'

export default {

  data () {
    return {
      icons,
      search: ''
    }
  },

  computed: {

    _search () {
      return this.search.toLowerCase()
    },

    matchedIcons () {
      return icons.filter(icon => this.match(icon))
    }
  },

  methods: {

    match (icon) {
      // Note: all filters and aliases are lowercase already
      return icon.name.toLowerCase().includes(this._search) ||                    /* eslint no-mixed-operators: "off" */
        icon.filter  && icon.filter.some(s => s.includes(this._search)) ||
        icon.aliases && icon.aliases.some(s => s.includes(this._search))
    },

    click (icon) {
      this.$emit('icon-select', icon)
    }
  }
}
</script>

<style>
.font-awesome-search .el-input {
  margin-bottom: 2em;
}

.font-awesome-search .el-button {
  font-size: 24px !important;
  color: var(--color-topic-icon);
  margin-left: 0 !important;    /* Element UI default is 10px */
  margin-right: 3px;
  margin-bottom: 3px;
}
</style>
