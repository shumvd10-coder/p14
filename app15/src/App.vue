<template>
<div class="container mt-5">
<h1 class="text-center mb-4">Моя коллекция</h1>
<div class="row">
<div class="col-md-8 offset-md-2">
<form @submit.prevent="addBook" class="card p-4 mb-4 shadow-sm">
<div class="mb-3">
<input v-model="newBook.title" type="text" class="form-control" placeholder="Название книги" required>
</div>
<div class="mb-3">
<textarea v-model="newBook.description" class="form-control" placeholder="Описание" required></textarea>
</div>
<div class="mb-3">
<input v-model="newBook.image" type="text" class="form-control" placeholder="Ссылка на фото" required>
</div>
<button class="btn btn-primary" type="submit">Добавить в коллекцию</button>
</form>
<div class="d-flex justify-content-end mb-3">
<button @click="sortBooks" class="btn btn-outline-secondary">Сортировать по названию</button>
</div>
</div>
</div>
<div class="row">
<div v-for="book in books" :key="book.id" class="col-md-4 mb-4">
<div class="card h-100 shadow-sm">
<img :src="book.image" class="card-img-top" alt="Обложка">
<div class="card-body d-flex flex-column">
<h5 class="card-title">{{ book.title }}</h5>
<p class="card-text">{{ book.description }}</p>
<button @click="removeBook(book.id)" class="btn btn-danger mt-auto">Удалить</button>
</div>
</div>
</div>
</div>
</div>
</template>

<script setup>
import { ref } from 'vue'

const books = ref([])
const newBook = ref({ title: '', description: '', image: '' })
const isSorted = ref(false)

const addBook = () => {
books.value.push({
id: Date.now(),
title: newBook.value.title,
description: newBook.value.description,
image: newBook.value.image
})
newBook.value.title = ''
newBook.value.description = ''
newBook.value.image = ''
}

const removeBook = (id) => {
books.value = books.value.filter(book => book.id !== id)
}

const sortBooks = () => {
isSorted.value = !isSorted.value
books.value.sort((a, b) => {
if (isSorted.value) {
return a.title.localeCompare(b.title)
}
return b.title.localeCompare(a.title)
})
}
</script>