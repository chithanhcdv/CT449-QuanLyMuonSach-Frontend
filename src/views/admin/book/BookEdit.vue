<template>
    <div v-if="book" class="page">
        <h4 class="edit-title">Hiệu chỉnh sách</h4>
        <BookForm
            :book="book"
            @submit:book="updateBook"
            @delete:book="deleteBook"
        />
        <p>{{ message }}</p>
    </div>
</template>

<script>
import BookForm from '@/components/admin/book/BookForm.vue';
import BookService from "@/services/book.service";

export default {
    components: {
        BookForm,
    },
    props: {
        id: { type: String, required: true },
    },
    data() {
        return {
            book: null,
            message: "",
        };
    },
    methods: {
        async getBook(id) {
            try {
                this.book = await BookService.getById(id);
            } catch (error) {
                console.log(error);
                this.$router.push({
                    name: "notfound",
                    params: {
                        pathMatch: this.$router.path.split("/").slice(1)
                    },
                    query: this.$route.query,
                    hash: this.$route.hash,
                });
            }
        },

        async updateBook(data) {
            try {
                await BookService.update(this.book._id, data);
                alert("Sách đã được cập nhật thành công");
                this.$router.push({ name: "book" });
            } catch (error) {
                console.log(error);
            }
        },

        async deleteBook() {
            if (confirm("Bạn muốn xóa Sách này?")) {
                try {
                    await BookService.delete(this.book._id);
                    alert("Sách đã được xóa thành công");
                    this.$router.push({ name: "book" });
                } catch (error) {
                    console.log(error);
                }
            }
        },
    },
    
    created() {
        this.getBook(this.id);
        this.message = "";
    },
};
</script>
