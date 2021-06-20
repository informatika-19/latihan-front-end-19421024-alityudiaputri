<template>
  <div class="q-pa-md" style="max-width: 400px">
    <q-form @submit="onSubmit" class="q-gutter-md">
      <q-input
        filled
        v-model="NamaKegiatan"
        label="Nama Kegiatan"
        hint="Nama Kegiatan"
        lazy-rules
        :rules="[
          val => (val && val.length > 0) || 'Nama Kegiatan Tidak Bpleh Kosang!'
        ]"
      />
      <q-input
        filled
        v-model="Deskripsi"
        label="Deskripsi Kegiatan"
        hint="Deskripsi Kegiatan"
        lazy-rules
        :rules="[
          val =>
            (val && val.length > 0) || 'Deskripsi Kegiatan Tidak Bpleh Kosang!'
        ]"
      />

      <q-input
        filled
        v-model="Waktu"
        label="Waktu Kegiatan"
        hint="Waktu Kegiatan"
        lazy-rules
        :rules="[
          val => (val && val.length > 0) || 'Waktu Kegiatan Tidak Bpleh Kosang!'
        ]"
      />

      <div>
        <q-btn label="Simpan Kegiatan" type="submit" color="primary" />
      </div>
    </q-form>
  </div>
</template>
<script>
export default {
  data () {
    return {
      NamaKegiatan: null,
      Deskripsi: null,
      Waktu: null
    }
  },
  methods: {
    onSubmit () {
      this.$axios
        .post('kegiatan/insert', {
          NamaKegiatan: this.NamaKegiatan,
          Deskripsi: this.Deskripsi,
          Waktu: this.Waktu
        })
        .then(res => {
          if (res.data.status) {
            this.$showNotif(res.data.pesan, 'positive')
            this.$router.push({ name: 'tampilKegiatan' })
          } else {
            this.$showNotif(res.data.pesan, 'negative')
          }
        })
    }
  }
}
</script>
