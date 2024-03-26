<template>
    <div class="page">
        <h4>Thêm Liên Hệ Mới</h4>
        <ContactForm :contact="contact" @submit:contact="(data) => createContact(data)"></ContactForm>
        <p>{{ message }}</p>
    </div>  
</template>

<script>
import ContactForm from '@/components/ContactForm.vue';
import ContactService from '@/services/contact.service';

export default{
    components: { ContactForm },
    data(){
        return{
            contact: null,
            message: ''
        }
    },
    methods: {
        async createContact(data){
            try{
                await ContactService.create(data)
                this.message = 'Thêm liên hệ thành công.'
            } catch(error) {
                console.log(error)
            }
        }
    },
    created() {
        this.contact = {
            name: undefined,
            email: undefined,
            phone: undefined,
            address: undefined,
            favorite: false
        },
        this.message = ''
    }
}
</script>