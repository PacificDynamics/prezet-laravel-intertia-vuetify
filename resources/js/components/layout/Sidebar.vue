<template>
  <v-navigation-drawer
    id="sidebar"
    v-model="drawer"
    dark
    color="#4A5568"
    app
    :clipped="true"
  >
    <v-list dense>
      <v-list-item v-if="$page.auth.user" two-line>
        <v-list-item-avatar>
          <v-img :src="gravatar" aspect-ratio="1" />
        </v-list-item-avatar>
        <v-list-item-content>
          <v-list-item-title>
            {{ $page.auth.user.name }}
          </v-list-item-title>
          <v-list-item-subtitle>
            {{ $page.auth.user.email }}
          </v-list-item-subtitle>
        </v-list-item-content>
      </v-list-item>

      <v-select
        v-model="teamId"
        clearable
        filled
        :loading="loading"
        label="Teams"
        :items="teams"
        item-text="name"
        item-value="id"
        :menu-props="{ closeOnContentClick: false}"
      >
        <template v-slot:append-item>
          <inertia-link class="v-list-item v-list-item--link theme--light" :href="route('settings')" method="get" @click="$emit('input')">
            <v-list-item-action>
              <fa icon="cog" />
            </v-list-item-action>
            <v-list-item-content>
              <v-list-item-title>
                Settings
              </v-list-item-title>
            </v-list-item-content>
          </inertia-link>
        </template>
      </v-select>

      <!-- settings -->
      <inertia-link class="v-list-item v-list-item--link theme--dark" :href="route('home')" method="get">
        <v-list-item-action>
          <fa icon="home" />
        </v-list-item-action>
        <v-list-item-content>
          <v-list-item-title>
            Home
          </v-list-item-title>
        </v-list-item-content>
      </inertia-link>

      <!-- settings -->
      <inertia-link class="v-list-item v-list-item--link theme--dark" :href="route('settings')" method="get">
        <v-list-item-action>
          <fa icon="cog" />
        </v-list-item-action>
        <v-list-item-content>
          <v-list-item-title>
            Settings
          </v-list-item-title>
        </v-list-item-content>
      </inertia-link>
    </v-list>
  </v-navigation-drawer>
</template>
<script>

export default {
  components: {
    //
  },
  props: {
    drawer: {
      type: Boolean,
      required: true,
    }
  },

  data: () => ({
    teamId: null,
    teams: [
      {
        id: 1,
        name: 'test'
      }
    ],
    loading: false
  }),

  computed: {
    gravatar () {
      return 'https://www.gravatar.com/avatar/' + this.$page.auth.user.gravatar
    }
  },
  methods: {
    hasPermission () {
      return true
    },
  }
}
</script>
