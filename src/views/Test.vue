<template>
  <div class="visual-tester">
    <button id="leaveTest" @click="gohome()">
      <font-awesome-icon icon="chevron-left" size="lg" fixed-width />
      {{ $t('message.tester.back.label') }}
    </button>
    <button
      id="resetTest"
      @click="reset()"
      :title="$t('message.tester.reset.title')"
    >
      <font-awesome-icon icon="undo" size="lg" fixed-width />
      {{ $t('message.tester.reset.label') }}
    </button>
    <!--h2 class="keyboardTesterTitle">{{ $t('message.tester.page.label') }}</h2-->
    <VisualTesterKeymap></VisualTesterKeymap>
  </div>
</template>

<script>
import { mapState, mapMutations } from 'vuex';
import VisualTesterKeymap from '@/components/VisualTesterKeymap';
export default {
  name: 'testerator',
  computed: {
    ...mapState('app', ['keyboard', 'layout'])
  },
  components: { VisualTesterKeymap },
  methods: {
    ...mapMutations('tester', ['reset']),
    gohome() {
      this.$router.push(`/${this.keyboard}/${this.layout}`);
    }
  }
};
</script>
<style></style>
