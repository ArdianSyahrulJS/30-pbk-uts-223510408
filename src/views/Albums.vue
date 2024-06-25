<template>
  <div class="albums">
    <div class="album-table">
      <div class="album-header">
        <span>Judul Album</span>
      </div>
      <div class="album-rows">
        <div v-for="album in albums" :key="album.id" class="album-row">
          <router-link :to="'/albums/' + album.id">{{ album.title }}</router-link>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { defineComponent, ref, onMounted } from 'vue';
import { useAlbumsStore } from '../store/album';

export default defineComponent({
  setup() {
    const albums = ref([]);
    const albumsStore = useAlbumsStore();

    onMounted(async () => {
      await albumsStore.fetchAlbums();
      albums.value = albumsStore.albums;
    });

    return {
      albums,
    };
  },
});
</script>

<style scoped>
.albums {
  max-width: 100%;
  margin: 0 auto;
  padding: 20px;
  text-align: center;
  margin-top: 50px;
  margin-bottom: 50px;
  color: #333;
  font-size: 20px;
  background: #f5f5dc;
  border-radius: 8px;
}

.album-table {
  display: flex;
  flex-direction: column;
  gap: 10px;
  border-radius: 5px;
  overflow: hidden;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.album-header {
  display: flex;
  justify-content: center;
  font-weight: bold;
  border-bottom: 2px solid #333;
  padding: 15px;
  background-color: #a0522d;
  color: #f5f5dc;
}

.album-rows {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 10px;
  justify-items: center;
}

.album-row {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 15px;
  border: 1px solid #f5f5dc;
  border-top: none;
  transition: background-color 0.3s, transform 0.3s;
  background-color: rgba(160, 82, 45, 0.7);
  min-width: 200px;
  margin: 5px;
}

.album-row a {
  text-decoration: none;
  color: #f5f5dc;
  font-size: 1.1rem;
}

.album-row:hover {
  background-color: rgba(245, 245, 220, 0.1);
  transform: translateY(-2px);
  border-color: #f5f5dc;
}
</style>
