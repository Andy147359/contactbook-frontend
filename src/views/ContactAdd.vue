<template>
    <div class="page">
        <h4>Thêm Mới Liên Hệ</h4>
        <ContactForm :contact="newContact" @submit:contact="addContact" />
    </div>
</template>

<script>
import ContactForm from "@/components/ContactForm.vue";
import ContactService from "@/services/contact.service";

export default {
    components: {
        ContactForm,
    },
    data() {
        return {
            newContact: {
                name: '',
                email: '',
                address: '',
                phone: '',
                favorite: false,
            },
        };
    },
    methods: {
        async addContact(data) {
            try {
                // Gọi API để thêm liên hệ mới
                await ContactService.create(data);
                alert('Liên hệ đã được thêm thành công.');
                // Quay về trang ContactBook sau khi thêm thành công
                this.$router.push({ name: "contactbook" });
            } catch (error) {
                console.log(error);
            }
        },
    },
};
</script>