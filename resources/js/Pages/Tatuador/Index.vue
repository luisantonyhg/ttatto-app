<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import {Head, useForm, usePage} from '@inertiajs/vue3';
import Create from "@/Pages/Tatuador/Partials/Create.vue";
import PrimaryButton from "@/Components/PrimaryButton.vue";
import Modal from "@/Components/Modal.vue";
import {ref} from "vue";
import Update from "@/Pages/Tatuador/Partials/Update.vue";
import InputError from "@/Components/InputError.vue";
import InputLabel from "@/Components/InputLabel.vue";
import TextInput from "@/Components/TextInput.vue";

defineProps({
    tatuadores: {
        type: Array
    }
});


const form = useForm({
    id: '',
    nombres: '',
    dni: '',
});

const stateModalRegistro = ref(false)
const stateModalUpdate = ref(false)
const id = ref('')
const nombres = ref('')
const dni = ref('')

const openModalRegistro = () => stateModalRegistro.value = true;
const openModalUpdate = (tatuador) => {

    stateModalUpdate.value = true;
    form.id = tatuador.id
    form.nombres = tatuador.nombres
    form.dni = tatuador.dni

}
const closeModalRegistro = () => stateModalRegistro.value = false
const closeModalUpdate = () => stateModalUpdate.value = false


const update = () => {
    form.put(route('tatuador.update'), {
        preserveScroll: true,
        onSuccess: () => {
            form.reset()
            stateModalUpdate.value = false
        },
        onError: () => {
            if (form.errors.nombres) {
                form.reset('nombres', 'dni');

            }
            if (form.errors.dni) {
                form.reset('dni');
            }
        },
    });
};

const eliminar = (tatuador) => {
    form.id = tatuador.id
    form.nombres = tatuador.nombres
    form.dni = tatuador.dni

    form.delete(route('tatuador.delete'), {
        preserveScroll: true,
        onSuccess: () => {

        },
        onError: () => {

        },
        onFinish: () => form.reset(),
    });
}

</script>

<template>
    <Head title="Tatuador"/>


    <AuthenticatedLayout>
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">PERFIL : {{ $page.props.auth.user.role }}</h2>
        </template>
        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8 space-y-6">
                <div class="p-4 sm:p-8 bg-white shadow sm:rounded-lg">
                    <section>
                        <div class="bg-white overflow-hidden shadow-sm sm:rounded-lg">
                            <div class="container py-10 px-10 mx-0 min-w-full flex flex-col items-center">
                                <h2 class="text-5xl mb-3 text-black">Tatuadores</h2>
                                <button @click="openModalRegistro"
                                        class="bg-purple-900 text-white hover:bg-blue-400 font-bold py-2 px-4 mt-3 rounded">
                                    Agregar tatuador
                                </button>
                            </div>
                        </div>
                        <div
                            class="rounded-sm border border-stroke bg-white px-5 pt-6 pb-2.5 shadow-default dark:border-strokedark dark:bg-boxdark sm:px-7.5 xl:pb-1">
                            <div class="max-w-full overflow-x-auto">

                                <table class="w-full table-auto">
                                    <thead>
                                    <tr class="bg-gray-2 text-left dark:bg-meta-4">
                                        <th class="min-w-[220px] py-4 px-4 font-medium text-black dark:text-white xl:pl-11">#</th>
                                        <th class="min-w-[220px] py-4 px-4 font-medium text-black dark:text-white xl:pl-11">Nombres</th>
                                        <th class="min-w-[220px] py-4 px-4 font-medium text-black dark:text-white xl:pl-11">Nro. DNI</th>
                                        <th class="min-w-[220px] py-4 px-4 font-medium text-black dark:text-white xl:pl-11">Estado</th>
                                        <th class="min-w-[220px] py-4 px-4 font-medium text-black dark:text-white xl:pl-11">Acciones</th>
                                    </tr>
                                    </thead>
                                    <tbody>
                                    <tr v-for="(tatuador, index) in $page.props.tatuadores">
                                        <td class="border-b border-[#eee] py-5 px-4 pl-9 dark:border-strokedark xl:pl-11">{{ index++ + 1 }}</td>
                                        <td class="border-b border-[#eee] py-5 px-4 pl-9 dark:border-strokedark xl:pl-11">{{ tatuador.nombres }}</td>
                                        <td class="border-b border-[#eee] py-5 px-4 pl-9 dark:border-strokedark xl:pl-11">{{ tatuador.dni }}</td>
                                        <td class="border-b border-[#eee] py-5 px-4 pl-9 dark:border-strokedark xl:pl-11">
                                            <p :class=" `${tatuador.estado === 'ACTIVO' ? 'text-green-500' : 'text-red-500'}` ">
                                                {{ tatuador.estado }}
                                            </p>
                                        </td>
                                        <td class="border-b border-[#eee] py-5 px-4 pl-9 dark:border-strokedark xl:pl-11">
                                            <button  @click="openModalUpdate(tatuador)"
                                                     class="hover:text-primary">
                                                <svg class="fill-current" width="18" height="18" viewBox="0 0 18 18" fill="none" xmlns="http://www.w3.org/2000/svg">
                                                    <path d="M8.99981 14.8219C3.43106 14.8219 0.674805 9.50624 0.562305 9.28124C0.47793 9.11249 0.47793 8.88749 0.562305 8.71874C0.674805 8.49374 3.43106 3.20624 8.99981 3.20624C14.5686 3.20624 17.3248 8.49374 17.4373 8.71874C17.5217 8.88749 17.5217 9.11249 17.4373 9.28124C17.3248 9.50624 14.5686 14.8219 8.99981 14.8219ZM1.85605 8.99999C2.4748 10.0406 4.89356 13.5562 8.99981 13.5562C13.1061 13.5562 15.5248 10.0406 16.1436 8.99999C15.5248 7.95936 13.1061 4.44374 8.99981 4.44374C4.89356 4.44374 2.4748 7.95936 1.85605 8.99999Z" fill=""></path>
                                                    <path d="M9 11.3906C7.67812 11.3906 6.60938 10.3219 6.60938 9C6.60938 7.67813 7.67812 6.60938 9 6.60938C10.3219 6.60938 11.3906 7.67813 11.3906 9C11.3906 10.3219 10.3219 11.3906 9 11.3906ZM9 7.875C8.38125 7.875 7.875 8.38125 7.875 9C7.875 9.61875 8.38125 10.125 9 10.125C9.61875 10.125 10.125 9.61875 10.125 9C10.125 8.38125 9.61875 7.875 9 7.875Z" fill=""></path>
                                                </svg>
                                            </button>

                                            <button @click="eliminar(tatuador)"
                                                    class="hover:text-primary">
                                                <svg class="fill-current" width="18" height="18" viewBox="0 0 18 18" fill="none" xmlns="http://www.w3.org/2000/svg">
                                                    <path d="M13.7535 2.47502H11.5879V1.9969C11.5879 1.15315 10.9129 0.478149 10.0691 0.478149H7.90352C7.05977 0.478149 6.38477 1.15315 6.38477 1.9969V2.47502H4.21914C3.40352 2.47502 2.72852 3.15002 2.72852 3.96565V4.8094C2.72852 5.42815 3.09414 5.9344 3.62852 6.1594L4.07852 15.4688C4.13477 16.6219 5.09102 17.5219 6.24414 17.5219H11.7004C12.8535 17.5219 13.8098 16.6219 13.866 15.4688L14.3441 6.13127C14.8785 5.90627 15.2441 5.3719 15.2441 4.78127V3.93752C15.2441 3.15002 14.5691 2.47502 13.7535 2.47502ZM7.67852 1.9969C7.67852 1.85627 7.79102 1.74377 7.93164 1.74377H10.0973C10.2379 1.74377 10.3504 1.85627 10.3504 1.9969V2.47502H7.70664V1.9969H7.67852ZM4.02227 3.96565C4.02227 3.85315 4.10664 3.74065 4.24727 3.74065H13.7535C13.866 3.74065 13.9785 3.82502 13.9785 3.96565V4.8094C13.9785 4.9219 13.8941 5.0344 13.7535 5.0344H4.24727C4.13477 5.0344 4.02227 4.95002 4.02227 4.8094V3.96565ZM11.7285 16.2563H6.27227C5.79414 16.2563 5.40039 15.8906 5.37227 15.3844L4.95039 6.2719H13.0785L12.6566 15.3844C12.6004 15.8625 12.2066 16.2563 11.7285 16.2563Z" fill=""></path>
                                                    <path d="M9.00039 9.11255C8.66289 9.11255 8.35352 9.3938 8.35352 9.75942V13.3313C8.35352 13.6688 8.63477 13.9782 9.00039 13.9782C9.33789 13.9782 9.64727 13.6969 9.64727 13.3313V9.75942C9.64727 9.3938 9.33789 9.11255 9.00039 9.11255Z" fill=""></path>
                                                    <path d="M11.2502 9.67504C10.8846 9.64692 10.6033 9.90004 10.5752 10.2657L10.4064 12.7407C10.3783 13.0782 10.6314 13.3875 10.9971 13.4157C11.0252 13.4157 11.0252 13.4157 11.0533 13.4157C11.3908 13.4157 11.6721 13.1625 11.6721 12.825L11.8408 10.35C11.8408 9.98442 11.5877 9.70317 11.2502 9.67504Z" fill=""></path>
                                                    <path d="M6.72245 9.67504C6.38495 9.70317 6.1037 10.0125 6.13182 10.35L6.3287 12.825C6.35683 13.1625 6.63808 13.4157 6.94745 13.4157C6.97558 13.4157 6.97558 13.4157 7.0037 13.4157C7.3412 13.3875 7.62245 13.0782 7.59433 12.7407L7.39745 10.2657C7.39745 9.90004 7.08808 9.64692 6.72245 9.67504Z" fill=""></path>
                                                </svg>
                                            </button>
                                        </td>
                                    </tr>
                                    </tbody>
                                </table>
                            </div>
                        </div>
                    </section>

                </div>
                <Modal :show="stateModalRegistro" @close="closeModalRegistro">
                    <Create/>
                </Modal>

                <Modal :show="stateModalUpdate" @close="closeModalUpdate">
                    <div class="py-12">
                        <div class="max-w-7xl mx-auto sm:px-6 lg:px-8 space-y-6">
                            <div class="p-4 sm:p-8 bg-white shadow sm:rounded-lg">
                                <section>
                                    <header>
                                        <h2 class="text-lg font-medium text-gray-900">Editar Tatuador</h2>
                                    </header>

                                    <form @submit.prevent="update" class="mt-6 space-y-6">
                                        <div>
                                            <InputLabel for="nombres" value="Nombres"/>

                                            <TextInput
                                                id="nombres"
                                                type="text"
                                                class="mt-1 block w-full"
                                                v-model="form.nombres"
                                                autofocus
                                                autocomplete="nombres"
                                            />

                                            <InputError class="mt-2" :message="form.errors.nombres"/>
                                        </div>

                                        <div>
                                            <InputLabel for="dni" value="Nro DNI"/>

                                            <TextInput
                                                id="dni"
                                                type="text"
                                                class="mt-1 block w-full"
                                                v-model="form.dni"
                                                autocomplete="dni"
                                            />

                                            <InputError class="mt-2" :message="form.errors.dni"/>
                                        </div>

                                        <div class="flex items-center gap-4">
                                            <PrimaryButton :disabled="form.processing">Actualizar</PrimaryButton>

                                            <Transition enter-from-class="opacity-0" leave-to-class="opacity-0"
                                                        class="transition ease-in-out">
                                                <p v-if="form.recentlySuccessful" class="text-sm text-gray-600">
                                                    Editado.</p>
                                            </Transition>
                                        </div>
                                    </form>
                                </section>
                            </div>
                        </div>
                    </div>
                </Modal>

            </div>
        </div>
    </AuthenticatedLayout>
</template>
