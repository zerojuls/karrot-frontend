<template>
  <span v-if="currentGroup">
    <q-toolbar v-if="$q.platform.is.mobile">
      <q-toolbar-title>{{ currentGroup.name }}</q-toolbar-title>
      <CommunityFeed />
      <LocaleSelect />
      <q-btn
        flat
        dense
        round
        :to="{ name: 'groupsGallery' }"
        :title="$t('TOPBAR.CHANGE_GROUP')"
      >
        <q-icon name="fas fa-exchange-alt" />
        <q-tooltip v-t="'TOPBAR.CHANGE_GROUP'" />
      </q-btn>
    </q-toolbar>
    <SidenavMap v-if="!$q.platform.is.mobile"/>
    <SidenavGroup/>
    <SidenavStore/>
    <SidenavStores/>
  </span>
</template>

<script>
import SidenavMap from './SidenavMap'
import SidenavGroup from './SidenavGroup'
import SidenavStore from './SidenavStore'
import SidenavStores from './SidenavStores'

import LocaleSelect from '@/components/General/LocaleSelect'
import CommunityFeed from '@/components/General/CommunityFeed'

import { QToolbar, QToolbarTitle, QBtn, QIcon, QTooltip } from 'quasar'

import { mapGetters } from 'vuex'

export default {
  components: {
    QToolbar,
    QToolbarTitle,
    QBtn,
    QIcon,
    QTooltip,
    SidenavMap,
    SidenavGroup,
    SidenavStore,
    SidenavStores,
    LocaleSelect,
    CommunityFeed,
  },
  computed: {
    ...mapGetters({
      currentGroup: 'currentGroup/value',
    }),
  },
}
</script>
