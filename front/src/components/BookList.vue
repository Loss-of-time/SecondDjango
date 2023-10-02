<template>
    <div>
        <h1>Books</h1>
        <ul>
            <li v-for="book in books" :key="book.id">
                {{ book.title }} by {{ book.author }}
            </li>
        </ul>
        <form @submit.prevent="addBook">
            <label for="title">Title:</label>
            <input type="text" id="title" v-model="newBook.title" required>
            <label for="author">Author:</label>
            <input type="text" id="author" v-model="newBook.author" required>
            <label for="published_date">Published Date:</label>
            <input type="date" id="published_date" v-model="newBook.published_date" required>
            <label for="description">Description:</label>
            <textarea id="description" v-model="newBook.description" required></textarea>
            <button type="submit">Add Book</button>
        </form>
    </div>
</template>
  
<script setup lang="ts">
import { ref, reactive } from 'vue';
import axios, { AxiosResponse } from 'axios';

interface Book {
    id: number;
    title: string;
    author: string;
    published_date: string;
    description: string;
}

const books = ref<Book[]>([]);
const newBook = reactive<Book>({
    id: 0,
    title: '',
    author: '',
    published_date: '',
    description: '',
});

axios.get<Book[]>('http://127.0.0.1:8000/books/?format=json')
    .then((response: AxiosResponse<Book[]>) => {
        books.value = response.data;
        console.log(books.value);
    })
    .catch((error: Error) => {
        console.log(error);
    });

const addBook = (): void => {
    axios.post<Book>('http://localhost:8000/books/', newBook)
        .then((response: AxiosResponse<Book>) => {
            books.value.push(response.data);
            newBook.id = 0;
            newBook.title = '';
            newBook.author = '';
            newBook.published_date = '';
            newBook.description = '';
        })
        .catch((error: Error) => {
            console.log(error);
        });
};
</script>