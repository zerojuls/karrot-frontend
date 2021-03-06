<template>
  <q-list
    highlight
    no-border
    class="no-padding"
  >
    <q-item
      v-for="store in stores"
      :key="store.id"
      link
      :to="linkParamsFor(store)"
    >
      <q-item-side class="text-center">
        <q-icon
          :name="store.ui.icon"
          :color="store.ui.color"
          :title="$t(store.ui.label)"
        />
      </q-item-side>
      <q-item-main>
        <q-item-tile label>
          {{ store.name }}
        </q-item-tile>
      </q-item-main>
    </q-item>

    <q-item
      v-if="!hasStores"
      link
      :to="{ name: 'storeCreate', params: { groupId } }"
      class="bg-secondary"
      multiline
    >
      <q-item-main class="text-center">
        <q-item-tile
          icon="add circle"
          class="text-white"
        />
        <q-tooltip v-t="'BUTTON.CREATE'" />
      </q-item-main>
    </q-item>

    <q-item-separator v-if="archived.length > 0" />

    <q-collapsible
      v-if="archived.length > 0"
      icon="fas fa-trash-alt"
      :label="`${$t('STORESTATUS.ARCHIVED')} (${archived.length})`"
    >
      <q-item
        v-for="store in archived"
        :key="store.id"
        link
        :to="linkParamsFor(store)"
      >
        <q-item-main>
          <q-item-tile label>
            {{ store.name }}
          </q-item-tile>
        </q-item-main>
      </q-item>
    </q-collapsible>
  </q-list>
</template>

<script>
import { QList, QListHeader, QItem, QItemMain, QItemTile, QItemSide, QIcon, QTooltip, QCollapsible, QItemSeparator } from 'quasar'

export default {
  components: { QList, QListHeader, QItem, QItemMain, QItemTile, QItemSide, QIcon, QTooltip, QCollapsible, QItemSeparator },
  props: {
    groupId: { required: true, type: Number },
    stores: { required: true, type: Array },
    archived: { default: () => [], type: Array },
    linkTo: { default: 'store', type: String },
  },
  computed: {
    hasStores () {
      return this.stores && this.stores.length > 0
    },
  },
  methods: {
    linkParamsFor (store) {
      return {
        name: this.linkTo,
        params: {
          groupId: store.group.id,
          storeId: store.id,
        },
      }
    },
  },
}
</script>
