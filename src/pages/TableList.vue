<template>
  <div class="container">
    <div class="row">
      <div class="col-md-3" v-for="(book, index) in books" :key="index">
        <div class="card mb-4 shadow-sm card-equal-height">
          <img :src="book.image" class="card-img-top" alt="Book Cover" />
          <div class="card-body">
            <h5 class="card-title">{{ book.judul }}</h5>
            <p class="card-text">Kategori: {{ book.kategori }}</p>
            <p class="card-text">ID Buku: {{ book.id }}</p>
            <div class="d-flex justify-content-between align-items-center">
              <button class="btn btn-success btn-sm" @click="editBook(book)">
                <i class="fas fa-edit"></i> Edit
              </button>
              <button class="btn btn-danger btn-sm" @click="confirmDelete(book.id)">
                <i class="fas fa-trash-alt"></i> Delete
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Swal from "sweetalert2";

export default {
  data() {
    return {
      books: [
        {
          id: "B001",
          judul: "Business is Fun",
          kategori: "bisnis",
          image: "https://via.placeholder.com/150",
        },
        {
          id: "B002",
          judul: "Digital Marketing Strategy",
          kategori: "bisnis",
          image: "https://via.placeholder.com/150",
        },
        {
          id: "B003",
          judul: "Filosofi Teras",
          kategori: "filsafat",
          image: "https://via.placeholder.com/150",
        },
        {
          id: "B004",
          judul: "Sejarah dunia yang disembunyikan",
          kategori: "sejarah",
          image: "https://via.placeholder.com/150",
        },
        {
          id: "B005",
          judul: "Dasar-dasar pemrograman web",
          kategori: "pemrograman",
          image: "https://via.placeholder.com/150",
        },
      ],
    };
  },
  methods: {
    editBook(book) {
      // Logika untuk mengedit buku
      // Bisa diarahkan ke halaman edit atau menampilkan form edit di modal
      alert(`Edit Buku: ${book.judul}`);
    },
    confirmDelete(bookId) {
      Swal.fire({
        title: "Apakah Anda yakin?",
        text: "Buku yang dihapus tidak dapat dikembalikan!",
        icon: "warning",
        showCancelButton: true,
        confirmButtonColor: "#d33",
        cancelButtonColor: "#3085d6",
        confirmButtonText: "Ya, hapus!",
        cancelButtonText: "Batal",
      }).then((result) => {
        if (result.isConfirmed) {
          this.deleteBook(bookId);
          Swal.fire("Dihapus!", "Buku telah dihapus.", "success");
        }
      });
    },
    deleteBook(bookId) {
      // Logika untuk menghapus buku
      this.books = this.books.filter((book) => book.id !== bookId);
    },
  },
};
</script>

<style>
.container {
  margin-top: 20px;
}

.card-equal-height {
  height: 400px; /* Set the height for uniform cards */
}

.card-img-top {
  height: 200px; /* Fixed height for images */
  object-fit: cover; /* Ensure image covers the entire area without distortion */
}

.card-body {
  text-align: center;
}

.card-title {
  font-size: 16px;
  font-weight: bold;
}

.card-text {
  font-size: 14px;
}

.btn-sm {
  width: 48%;
}

/* Ensure the card content fills the height equally */
.card-body {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}
</style>
