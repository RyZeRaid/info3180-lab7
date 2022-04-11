<script>
import UploadForm from '@/components/UploadForm.vue'

export default {
    data() {
    return {
        message: "Hello World! Welcome to Onandi's VueJS",
        description : '',
        photo : undefined

    };
    },
    components: { UploadForm }
    };

</script>

<template>
        <UploadForm />
</template>