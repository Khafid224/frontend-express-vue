<script setup>

//import sidebar component
import SidebarMenu from '../../../components/SidebarMenu.vue'

</script>

<template>
    <div class="container mt-5 mb-5">
        <div class="row">
            <div class="col-md-3">
                <SidebarMenu />
            </div>
            <div class="col-md-9">
                <div class="card border-0 rounded shadow-sm">
                    <div class="card-header d-flex justify-content-between align-items-center">
                        <span>USERS</span>
                        <router-link :to="{ name: 'admin.users.create' }"
                            class="btn btn-sm btn-success rounded shadow-sm border-0">ADD USER</router-link>
                    </div>
                    <div class="card-body">
                        HALAMAN USERS INDEX
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>