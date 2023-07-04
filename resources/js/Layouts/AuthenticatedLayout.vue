<script setup>
import { ref } from 'vue';
import ApplicationLogo from '@/Components/ApplicationLogo.vue';
import Dropdown from '@/Components/Dropdown.vue';
import DropdownLink from '@/Components/DropdownLink.vue';
import NavLink from '@/Components/NavLink.vue';
import ResponsiveNavLink from '@/Components/ResponsiveNavLink.vue';
import { Link } from '@inertiajs/vue3';

const showingNavigationDropdown = ref(false);
</script>

<template>



    <div>
        <div class="min-h-screen bg-gray-100">
            <nav class="bg-white border-b border-gray-100">
        
           

                
            </nav>

            <aside id="default-sidebar" class="fixed top-0 left-0 z-40 w-64 h-screen transition-transform -translate-x-full sm:translate-x-0 bg-blue-500" aria-label="Sidebar">
                <div class="h-full px-3 py-4 overflow-y-auto bg-gray-50 dark:bg-gray-800 " style="background:rgb(169, 204, 227)">
                    <ul class="space-y-2 font-medium">
                        <div class="">
                                <Link :href="route('dashboard')">
                                    <ApplicationLogo 
                                        class=""
                                       />
                                 
                                    <br>
                                    <span class="ml-3" style="color: blue;">MI NOMBRE :</span>
                                    <hr>
                                    <span class="ml-3" style="color: blue;">{{ $page.props.auth.user.name}}</span>
                                    
                                </Link>
                            </div>
                      
                        <br>
                        <li>
                            <NavLink  class="flex items-center p-2 text-gray-900 rounded-lg dark:text-white hover:bg-gray-100 dark:hover:bg-gray-700" :href="route('dashboard')" :active="route().current('dashboard')" v-if="$page.props.auth.user.role === 'ADMIN' ">
                                <svg aria-hidden="true" class="w-6 h-6 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path d="M2 10a8 8 0 018-8v8h8a8 8 0 11-16 0z"></path><path d="M12 2.252A8.014 8.014 0 0117.748 8H12V2.252z"></path></svg>
                                <span class="ml-3">CREAR CITAS</span>
                                    
                                </NavLink>
                        </li>
                        <br>
                        <li>
                            <NavLink  class="flex items-center p-2 text-gray-900 rounded-lg dark:text-white hover:bg-gray-100 dark:hover:bg-gray-700" :href="route('tatuador.index')" :active="route().current('tatuador.index')" v-if="$page.props.auth.user.role === 'ADMIN' ">
                                <svg aria-hidden="true" class="w-6 h-6 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path d="M2 10a8 8 0 018-8v8h8a8 8 0 11-16 0z"></path><path d="M12 2.252A8.014 8.014 0 0117.748 8H12V2.252z"></path></svg>
                                <span class="ml-3">TATUADOR</span>
                                    
                                </NavLink>
                        </li>
                        <br>
                        <li>
                            <NavLink  class="flex items-center p-2 text-gray-900 rounded-lg dark:text-white hover:bg-gray-100 dark:hover:bg-gray-700" :href="route('cita.index')" :active="route().current('cita.index')" v-if="$page.props.auth.user.role === 'ADMIN' ">
                                <svg aria-hidden="true" class="w-6 h-6 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path d="M2 10a8 8 0 018-8v8h8a8 8 0 11-16 0z"></path><path d="M12 2.252A8.014 8.014 0 0117.748 8H12V2.252z"></path></svg>
                                <span class="ml-3">TODAS LAS CITAS</span>
                                    
                                </NavLink>
                        </li>
                       
                        <br>
                        <li>
                            <NavLink  class="flex items-center p-2 text-gray-900 rounded-lg dark:text-white hover:bg-gray-100 dark:hover:bg-gray-700" :href="route('usuario.index')" :active="route().current('usuario.index')" v-if="$page.props.auth.user.role === 'ADMIN' " >
                                <svg aria-hidden="true" class="w-6 h-6 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path d="M2 10a8 8 0 018-8v8h8a8 8 0 11-16 0z"></path><path d="M12 2.252A8.014 8.014 0 0117.748 8H12V2.252z"></path></svg>
                                <span class="ml-3">USUARIOS CREADOS</span>
                                    
                                </NavLink>
                        </li>
                        <br>
                      
                        <li>
                            <NavLink  class="flex items-center p-2 text-gray-900 rounded-lg dark:text-white hover:bg-gray-100 dark:hover:bg-gray-700" :href="route('profile.edit')" :active="route().current('dashboard')" v-if="$page.props.auth.user.role === 'ADMIN' " >
                                <svg aria-hidden="true" class="w-6 h-6 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path d="M2 10a8 8 0 018-8v8h8a8 8 0 11-16 0z"></path><path d="M12 2.252A8.014 8.014 0 0117.748 8H12V2.252z"></path></svg>
                                <span class="ml-3">MI PERFIL</span>
                                    
                                </NavLink>
                        </li>
                        <br>
                        <li>
                            <NavLink  class="flex items-center p-2 text-gray-900 rounded-lg dark:text-white hover:bg-gray-100 dark:hover:bg-gray-700" :href="route('logout')" method="post" as="button"  v-if="$page.props.auth.user.role === 'ADMIN' ">
                                <svg aria-hidden="true" class="w-6 h-6 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path d="M2 10a8 8 0 018-8v8h8a8 8 0 11-16 0z"></path><path d="M12 2.252A8.014 8.014 0 0117.748 8H12V2.252z"></path></svg>
                                <span class="ml-3">CERRAR SESION</span>
                                    
                                </NavLink>
                        </li>
                        <br>
                        <li>
                            <NavLink  class="flex items-center p-2 text-gray-900 rounded-lg dark:text-white hover:bg-gray-100 dark:hover:bg-gray-700" :href="route('dashboard')" :active="route().current('dashboard')" v-if="$page.props.auth.user.role === 'USER' ">
                                <svg aria-hidden="true" class="w-6 h-6 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path d="M2 10a8 8 0 018-8v8h8a8 8 0 11-16 0z"></path><path d="M12 2.252A8.014 8.014 0 0117.748 8H12V2.252z"></path></svg>
                                <span class="ml-3">CREAR CITAS</span>
                                    
                                </NavLink>
                        </li>
                        <br>
                        <li>
                            <NavLink  class="flex items-center p-2 text-gray-900 rounded-lg dark:text-white hover:bg-gray-100 dark:hover:bg-gray-700" :href="route('profile.edit')" :active="route().current('dashboard')" v-if="$page.props.auth.user.role === 'USER' " >
                                <svg aria-hidden="true" class="w-6 h-6 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path d="M2 10a8 8 0 018-8v8h8a8 8 0 11-16 0z"></path><path d="M12 2.252A8.014 8.014 0 0117.748 8H12V2.252z"></path></svg>
                                <span class="ml-3">MI PERFIL</span>
                                    
                                </NavLink>
                        </li>
                        <br>
                        <li>
                            <NavLink  class="flex items-center p-2 text-gray-900 rounded-lg dark:text-white hover:bg-gray-100 dark:hover:bg-gray-700" :href="route('logout')" method="post" as="button"  v-if="$page.props.auth.user.role === 'USER' ">
                                <svg aria-hidden="true" class="w-6 h-6 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path d="M2 10a8 8 0 018-8v8h8a8 8 0 11-16 0z"></path><path d="M12 2.252A8.014 8.014 0 0117.748 8H12V2.252z"></path></svg>
                                <span class="ml-3">CERRAR SESION</span>
                                    
                                </NavLink>
                        </li>
                        
                    
                    </ul>
                </div>
              
                </aside>

        
            <header class="bg-white shadow" v-if="$slots.header"  style="background:rgb(169, 204, 227)">
                <div class="max-w-7xl mx-auto py-6 px-4 sm:px-6 lg:px-8">
                    <slot name="header" />
                </div>
            </header>

            
            <main>
                <slot />
            </main>
        </div>
    </div>
</template>
