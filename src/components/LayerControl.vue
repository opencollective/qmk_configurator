<template>
  <div>
    <p>
      <label>{{ $t('message.layer.label') }}:</label>
    </p>
    <div class="layers">
      <!-- prettier-ignore -->
      <div
        class="layer"
        :class="layer.clazz"
        v-for="layer in layers"
        :key="layer.id"
        @click="clicked(layer.id)"
      >{{ layer.name }}</div>
    </div>
    <button
      class="clear-button"
      :title="$t('message.layer.title')"
      @click="clearLayer"
    >
      <font-awesome-icon icon="trash" size="lg" fixed-width />
    </button>
  </div>
</template>
<script>
import rangeRight from 'lodash/rangeRight';
import isUndefined from 'lodash/isUndefined';
import { createNamespacedHelpers } from 'vuex';
const { mapState, mapGetters, mapMutations } = createNamespacedHelpers(
  'keymap'
);
export default {
  name: 'layer-control',
  computed: {
    ...mapState(['layer']),
    ...mapGetters(['getLayer']),
    layers() {
      let layers = rangeRight(16).map(layer => {
        let clazz = [layer];
        let _layer = this.getLayer(layer);
        if (!isUndefined(_layer)) {
          clazz.push('non-empty');
        }
        if (this.layer == layer) {
          clazz.push('active');
        }
        return {
          id: layer,
          name: layer,
          clazz: clazz.join(' ')
        };
      });

      return layers;
    }
  },
  methods: {
    ...mapMutations(['changeLayer', 'initLayer']),
    clicked(id) {
      if (isUndefined(this.getLayer(id))) {
        this.initLayer(id);
      }
      this.changeLayer(id);
    },
    clearLayer() {
      if (confirm(this.$t('message.layer.confirm'))) {
        this.initLayer(this.layer);
      }
    }
  }
};
</script>
<style scoped>
.clear-button {
  line-height: 100%;
  margin: 0;
  border-radius: 3px;
  background-color: #49ad4c;
  color: #fff;
  border: 0px solid #000;
  padding: 6px 8px;
  cursor: pointer;
}
</style>
