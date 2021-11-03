<template>
    <div class="new-form">
        <h4>Tạo mới Liên hệ</h4>
        <ContactForm
            :contact="{}"
            @contact-submit="updateContact"
        />
        <p>{{ message }}</p>
    </div>
</template>

<script>
import ContactService from "../services/contact.service";
import ContactForm from "../components/ContactForm";
export default {
    name: "ContactNew",
    components: {
        ContactForm,
    },
    data() {
        return {
            contact: null,
            message: "",
        };
    },
    methods: {
        async updateContact(data) {
            const [error, response] = await this.handle(
                ContactService.create(data)
            );
            if (error) {
                console.log(error);
            }
            else {
                console.log(response.data);
                this.message = "Liên hệ được tạo mới thành công.";
            }
        },
    },
    mounted() {
        this.message = "";
    },
};
</script>

<style>
.new-form {
    max-width: 400px;
    margin: auto;
}
</style>