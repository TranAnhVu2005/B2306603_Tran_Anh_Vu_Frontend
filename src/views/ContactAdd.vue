<template>
    <div class="page">
        <h4>Thêm liên hệ</h4>
        <ContactForm :contact="contact" @submit:contact="createContact"></ContactForm>
        <p>{{ message }}</p>
    </div>
</template>

<script>
import ContactForm from '@/components/ContactForm.vue';
import ContactService from '@/services/contact.service';
export default{
    components: {
        ContactForm,
    },
    data(){
        return {
            contact: {},
            message: "",
        };
    },
    methods: {
         async createContact(data){
            try {
                await ContactService.create(data);
                alert('Liên hệ được tạo thành công.');
                this.$router.push({name: "contactbook"});
            }
            catch(error){
                console.log(error);
            }
        },
    },
    created(){ // Bắt đầu vòng đời của component thì lấy contact rồi
        this.message = "";
    },
};

</script>