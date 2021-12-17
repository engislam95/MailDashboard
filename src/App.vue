<template>
  <q-layout
    view="hHh Lpr lff"
    container
    style="height: 100vh"
    class="shadow-2 rounded-borders"
  >
    <q-header elevated class="bg-white">
      <q-toolbar style="min-height: 60px">
        <q-toolbar-title>
          <img alt="Vue logo" src="./assets/logo-1.svg" />
          <span style="color: #0097a7; position: relative; top: -5px">
            MAIL IPSUM
          </span>
          <q-input
            style="display: inline-block; width: 30%; margin-left: 20px"
            v-model="search"
            debounce="500"
            filled
            :dense="true"
            color="amber-6"
            bg-color="cyan-1"
            placeholder="Search here..."
          >
            <template v-slot:prepend>
              <q-icon name="search" color="amber-6" />
            </template>
          </q-input>
        </q-toolbar-title>

        <q-btn dense color="cyan-8" flat icon="inbox" class="q-mr-md">
          <q-badge color="amber-6" floating rounded></q-badge>
        </q-btn>
        <q-icon name="settings" color="cyan-8" size="sm" class="q-mr-md" />
        <q-icon name="question_mark" color="cyan-8" size="sm" class="q-mr-md" />
        <q-chip
          flat
          square
          color="transparent"
          text-color="cyan-8"
          icon-right="more_vert"
        >
          John Alex
        </q-chip>
        <q-btn
          flat
          @click="drawer = !drawer"
          round
          dense
          icon="menu"
          color="cyan-8"
        />
      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="drawer"
      show-if-above
      :width="250"
      :breakpoint="500"
      bordered
      class="bg-cyan-8 text-white"
    >
      <q-scroll-area class="fit">
        <q-list>
          <q-btn
            color="cyan-9"
            class="compose"
            text-color="white"
            icon-color="amber-6"
            no-caps
            unelevated
            icon="mark_email_read"
            label="Compose Mail"
          />
          <template v-for="(menuItem, index) in menuList" :key="index">
            <q-item clickable :active="menuItem.label === 'Outbox'" v-ripple>
              <q-item-section avatar>
                <q-icon :name="menuItem.icon" />
              </q-item-section>
              <q-item-section>
                {{ menuItem.label }}
              </q-item-section>
            </q-item>
            <q-separator :key="'sep' + index" v-if="menuItem.separator" />
          </template>
        </q-list>
      </q-scroll-area>
    </q-drawer>

    <q-page-container>
      <q-page padding style="background: #f6f6fa">
        <router-view />
      </q-page>
    </q-page-container>
  </q-layout>
</template>
<script>
const menuList = [
  {
    icon: "inbox",
    label: "Inbox",
    separator: false,
  },
  {
    icon: "send",
    label: "Outbox",
    separator: false,
  },
  {
    icon: "delete",
    label: "Trash",
    separator: false,
  },
  {
    icon: "error",
    label: "Spam",
    separator: true,
  },
  {
    icon: "settings",
    label: "Settings",
    separator: false,
  },
  {
    icon: "feedback",
    label: "Send Feedback",
    separator: false,
  },
  {
    icon: "help",
    iconColor: "primary",
    label: "Help",
    separator: false,
  },
];

export default {
  data() {
    return {
      drawer: false,
      menuList,
      search: "",
    };
  },
};
</script>

<style lang="scss">
.compose {
  margin: 0 auto !important;
  display: flex !important;
  padding: 10px !important;
  margin-top: 20px !important;
  margin-bottom: 20px !important;
  i {
    color: #f9b52e !important;
  }
}
.q-item.q-router-link--active,
.q-item--active {
  background: linear-gradient(90deg, #2d9898 0%, #38a7a7 92.13%);
  border-left: 4px solid #f9b52e;
  color: #fff !important;
}
.cyan-9 {
  color: #38a7a7 !important;
}
.bg-cyan-9 {
  background: #38a7a7 !important;
}
.amber-6 {
  color: #f9b52e !important;
}
</style>
