<template>
  <div id="app">
    <q-layout view="hHh lpR fFf">
      <q-header elevated>
        <q-toolbar>
          <router-link to="/" exact-active-class="active" class="q-item" exact>
            <q-item-label>Kegiatan</q-item-label>
          </router-link>
          <router-link to="/posts" exact-active-class="active" class="q-item" exact>
            <q-item-label>Post</q-item-label>
          </router-link>
          <router-link to="/albums" exact-active-class="active" class="q-item" exact>
            <q-item-label>Album</q-item-label>
          </router-link>
        </q-toolbar>
      </q-header>
      
      <q-page-container>
        <router-view />
      </q-page-container>
    </q-layout>
  </div>
</template>

<script>
export default {
  name: 'App',
};
</script>

<style scoped>
* {
  font-family: Cambria, Cochin, Georgia, Times, 'Times New Roman', serif;
}

.q-header {
  background-color: #f5f5dc;
  color: #333;
  padding: 15px;
  font-size: 18px;
  border-radius: 2px;
}

.q-toolbar {
  justify-content: center;
}

.q-item.active {
  font-weight: bold;
  font-size: 18.5px;
}

.q-item {
  margin: 0 10px;
  text-decoration: none;
  color: inherit;
  justify-content: center;
  padding-bottom: 5px;
}
</style>