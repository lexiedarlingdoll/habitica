<template lang="pug">
.row
  secondary-menu.col-12
    router-link.nav-link(:to="{name: 'groupPlanDetailTaskInformation', params: {groupId}}",
      exact, :class="{'active': $route.name === 'groupPlanDetailTaskInformation'}") {{ $t('groupTaskBoard') }}
    router-link.nav-link(:to="{name: 'groupPlanDetailInformation', params: {groupId}}",
      exact, :class="{'active': $route.name === 'groupPlanDetailInformation'}") {{ $t('groupInformation') }}
    router-link.nav-link(
      v-if='isLeader',
      :to="{name: 'groupPlanBilling', params: {groupId}}",
      exact,
      :class="{'active': $route.name === 'groupPlanBilling'}") {{ $t('groupBilling') }}

  .col-12
    router-view
</template>

<script>
import SecondaryMenu from 'client/components/secondaryMenu';
import { mapState } from 'client/libs/store';

export default {
  props: ['groupId'],
  components: {
    SecondaryMenu,
  },
  computed: {
    ...mapState({
      user: 'user.data',
      groupPlans: 'groupPlans',
    }),
    isLeader () {
      let groupFound = this.groupPlans.find(group => {
        return group._id === this.groupId;
      });

      if (!groupFound) return false;
      return groupFound.leader === this.user._id;
    },
  },
};
</script>
