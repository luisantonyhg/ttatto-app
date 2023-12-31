<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import {Head, useForm} from '@inertiajs/vue3';
import TextInput from "@/Components/TextInput.vue";
import InputLabel from "@/Components/InputLabel.vue";
import PrimaryButton from "@/Components/PrimaryButton.vue";
import InputError from "@/Components/InputError.vue";
import {useToast} from 'vue-toast-notification';
import 'vue-toast-notification/dist/theme-bootstrap.css';
import {nextTick, ref} from "vue";
import Modal from "@/Components/Modal.vue";

const $toast = useToast();

const form = useForm({
    id: '',
});
const register = () => {

    form.post(route('mi-cita.store'), {
        preserveScroll: true,
        onSuccess: (value) => {

            form.reset()
        },
        onError: (errors) => {

            if (errors.create){
                $toast.error(`${errors.create}`, {
                    position: 'bottom'
                })
            }

            if (form.errors.id) {
                form.reset('id');
            }
        },
    });
}

const finalizar = (cita) => {
    form.id = cita.id
    form.put(route('cita.finalizar'), {
        preserveScroll: true,
        onSuccess: (value) => {
            $toast.success(`Cita finalizada exitosamente`, {
                position: 'bottom'
            })
            form.reset()
        },
        onError: (errors) => {

            if (errors.create){
                $toast.error(`${errors.create}`, {
                    position: 'bottom'
                })
            }

            if (form.errors.id) {
                form.reset('id');
            }
        },
    });
}

const reporte = (cita) => {
  
    window.open(`${APP_NAME}/citas/reporte/${cita.id}`, '_blank')
}

</script>

<template>
    <Head title="Mis citas" />

    <AuthenticatedLayout>
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">PERFIL :{{ $page.props.auth.user.role }}</h2>
        </template>
        <div class="py-12">

            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-white overflow-hidden shadow-sm sm:rounded-lg">
                    <div class="bg-white overflow-hidden shadow-sm sm:rounded-lg">
                        <div class="container py-10 px-10 mx-0 min-w-full flex flex-col items-center">
                            <h2 class="text-5xl mb-3 text-black">Citas</h2>
                        </div>
                    </div>
                    <div class="container py-10 px-10 mx-0 min-w-full">
                        <h2 class="text-3xl mb-3 text-black">Bandeja</h2>
                        <section>
                            <div class="rounded-sm border border-stroke bg-white px-5 pt-6 pb-2.5 shadow-default dark:border-strokedark dark:bg-boxdark sm:px-7.5 xl:pb-1">
                                <div class="max-w-full overflow-x-auto">
                                    <table class="w-full table-auto">
                                        <thead>
                                        <tr class="bg-gray-2 text-left dark:bg-meta-4">
                                            <th class="min-w-[100px] py-4 px-4 font-medium text-black dark:text-white xl:pl-11">
                                                #
                                            </th>
                                            <th class="min-w-[220px] py-4 px-4 font-medium text-black dark:text-white xl:pl-11" style="color: rgb(78, 165, 16);">
                                                Cliente
                                            </th>
                                            <th class="min-w-[150px] py-4 px-4 font-medium text-black dark:text-white xl:pl-11" style="color: rgb(78, 165, 16);">
                                                Fecha
                                            </th>
                                            <th class="min-w-[150px] py-4 px-4 font-medium text-black dark:text-white" style="color: rgb(78, 165, 16);">
                                                Hora Inicia
                                            </th>
                                            <th class="min-w-[150px] py-4 px-4 font-medium text-black dark:text-white" style="color: rgb(78, 165, 16);">
                                                Hora termina
                                            </th>
                                            <th class="min-w-[120px] py-4 px-4 font-medium text-black dark:text-white" style="color: rgb(78, 165, 16);">
                                                Tatuador
                                            </th>
                                            <th class="min-w-[120px] py-4 px-4 font-medium text-black dark:text-white" style="color: rgb(78, 165, 16);">
                                                Estado
                                            </th>
                                            <th class="py-4 px-4 font-medium text-black dark:text-white" style="color: rgb(78, 165, 16);">
                                                Acciones
                                            </th>
                                        </tr>
                                        </thead>
                                        <tbody>
                                        <tr v-for="(cita, index) in $page.props.citas">
                                            <td class="border-b border-[#eee] py-5 px-4 pl-9 dark:border-strokedark xl:pl-11">
                                                {{ index++ + 1 }}
                                            </td>
                                            <td class="border-b border-[#eee] py-5 px-4 pl-9 dark:border-strokedark xl:pl-11">
                                                <p class="text-sm">{{ cita.user.name }}</p>
                                            </td>
                                            <td class="border-b border-[#eee] py-5 px-4 pl-9 dark:border-strokedark xl:pl-11">
                                                <p class="text-sm">{{ cita.fecha }}</p>
                                            </td>
                                            <td class="border-b border-[#eee] py-5 px-4 dark:border-strokedark">
                                                <p class="text-black dark:text-white">{{ cita.hora }}</p>
                                            </td>
                                            <td class="border-b border-[#eee] py-5 px-4 dark:border-strokedark">
                                                <p class="text-black dark:text-white">{{ cita.horatermina }}</p>
                                            </td>
                                            <td class="border-b border-[#eee] py-5 px-4 dark:border-strokedark">
                                                <p class="inline-flex rounded-full bg-success bg-opacity-10 py-1 px-3 text-sm font-medium text-success">
                                                    {{ cita.tatuador.nombres }}
                                                </p>
                                            </td>
                                            <td class="border-b border-[#eee] py-5 px-4 dark:border-strokedark">
                                                <p :class=" `${cita.estado === 'ACTIVO' ? 'text-green-500' : 'text-red-500'}` ">
                                                    {{ cita.estado }}
                                                </p>
                                            </td>
                                            <td class="border-b border-[#eee] py-5 px-4 dark:border-strokedark">
                                                <div class="flex items-center space-x-3.5">
                                                    <button @click="finalizar(cita)" class="hover:text-primary">
                                                        <svg class="fill-current" width="18" height="18" viewBox="0 0 512 512" fill="none" xmlns="http://www.w3.org/2000/svg">
                                                            <path fill-rule="evenodd" clip-rule="evenodd" d="M167.764 122.509C193.057 105.756 223.389 96 256 96C344.366 96 416 167.634 416 256C416 288.611 406.244 318.943 389.491 344.236L167.764 122.509ZM122.509 167.764C105.756 193.057 96 223.389 96 256C96 344.366 167.634 416 256 416C288.611 416 318.943 406.244 344.236 389.491L122.509 167.764ZM256 32C132.288 32 32 132.288 32 256C32 379.712 132.288 480 256 480C379.712 480 480 379.712 480 256C480 132.288 379.712 32 256 32Z" fill="black"/>
                                                        </svg>
                                                    </button>
                                                    <button @click="reporte(cita)" class="hover:text-primary">
                                                        <svg class="fill-current" width="18" height="18" viewBox="0 0 18 18" fill="none" xmlns="http://www.w3.org/2000/svg">
                                                            <path d="M16.8754 11.6719C16.5379 11.6719 16.2285 11.9531 16.2285 12.3187V14.8219C16.2285 15.075 16.0316 15.2719 15.7785 15.2719H2.22227C1.96914 15.2719 1.77227 15.075 1.77227 14.8219V12.3187C1.77227 11.9812 1.49102 11.6719 1.12539 11.6719C0.759766 11.6719 0.478516 11.9531 0.478516 12.3187V14.8219C0.478516 15.7781 1.23789 16.5375 2.19414 16.5375H15.7785C16.7348 16.5375 17.4941 15.7781 17.4941 14.8219V12.3187C17.5223 11.9531 17.2129 11.6719 16.8754 11.6719Z" fill=""></path>
                                                            <path d="M8.55074 12.3469C8.66324 12.4594 8.83199 12.5156 9.00074 12.5156C9.16949 12.5156 9.31012 12.4594 9.45074 12.3469L13.4726 8.43752C13.7257 8.1844 13.7257 7.79065 13.5007 7.53752C13.2476 7.2844 12.8539 7.2844 12.6007 7.5094L9.64762 10.4063V2.1094C9.64762 1.7719 9.36637 1.46252 9.00074 1.46252C8.66324 1.46252 8.35387 1.74377 8.35387 2.1094V10.4063L5.40074 7.53752C5.14762 7.2844 4.75387 7.31252 4.50074 7.53752C4.24762 7.79065 4.27574 8.1844 4.50074 8.43752L8.55074 12.3469Z" fill=""></path>
                                                        </svg>
                                                    </button>
                                                </div>
                                            </td>
                                        </tr>
                                        </tbody>
                                    </table>
                                </div>
                            </div>
                        </section>
                    </div>
                </div>
            </div>
        </div>

    </AuthenticatedLayout>
</template>
