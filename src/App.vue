
<template>
    <div>
        <Toast />

        <div class="card">
            <Steps :model="items" aria-label="Form Steps" :readonly="false" />
        </div>

        <router-view v-slot="{Component}"  @prevPage="prevPage($event)" @nextPage="nextPage($event)" @complete="complete">
            <keep-alive>
                <component :is="Component" />
            </keep-alive>
        </router-view>
    </div>
</template>

<script setup>
import { ref } from "vue";
import { useRouter } from "vue-router";
import { useToast } from "primevue/usetoast";

const router = useRouter();
const toast = useToast();
const items = ref([
    {
        label: 'Instrumentos',
        to: "/"
    },
    {
        label: 'Serviços de Calibração',
        to: "/seat",
    },
    {
        label: 'Confirmação',
        to: "/confirmation",
    }
]);
const formObject = ref({});

const nextPage = (event) => {
    router.push(items.value[event.pageIndex + 1].to);
};
const prevPage = (event) => {
    router.push(items.value[event.pageIndex - 1].to);
};
const complete = () => {
    toast.add({severity:'success', summary:'Order submitted', detail: 'Dear, ' + formObject.value.firstname + ' ' + formObject.value.lastname + ' your order completed.'});
};
</script>

<style scoped>
::v-deep(b) {
    display: block;
}

::v-deep(.p-card-body) {
    padding: 2rem;
}
</style>