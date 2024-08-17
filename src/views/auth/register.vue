<script setup>
// Import reactive and ref from vue
import { reactive, ref } from 'vue'

// Import useRouter from vue-router
import { useRouter } from 'vue-router'

// Inisialisasi vue-router dengan Composition API
const router = useRouter()

// Import services API
import api from '../../services/api'

// State user
const user = reactive({
    name: '',
    email: '',
    password: '',
    password_confirmation: ''
})

// State validation
const validation = ref({ errors: [] })

// Method register
const register = async () => {
    try {
        // Call API register
        await api.post('/api/register', {
            name: user.name,
            email: user.email,
            password: user.password,
            password_confirmation: user.password_confirmation
        })

        // Redirect ke halaman login setelah sukses
        router.push({ name: 'login' })
    } catch (error) {
        // Assign validation value with error
        if (error.response && error.response.data && error.response.data.errors) {
            validation.value.errors = error.response.data.errors
        } else {
            validation.value.errors = [{ path: 'Unknown', msg: 'An unknown error occurred' }]
        }
    }
}
</script>

<template>
    <div class="row justify-content-center">
        <div class="col-md-5">
            <div class="card border-0 rounded shadow-sm">
                <div class="card-body">
                    <h4>REGISTER</h4>
                    <hr />
                    <div v-if="validation.errors.length" class="mt-2 alert alert-danger">
                        <ul class="mt-0 mb-0">
                            <li v-for="(error, index) in validation.errors" :key="index">
                                {{ `${error.path} : ${error.msg}` }}
                            </li>
                        </ul>
                    </div>
                    <form @submit.prevent="register">
                        <div class="row">
                            <div class="col-md-12 mb-3">
                                <div class="form-group">
                                    <label class="mb-1 fw-bold">Full Name</label>
                                    <input
                                        type="text"
                                        v-model="user.name"
                                        class="form-control"
                                        placeholder="Full Name"
                                    />
                                </div>
                            </div>
                        </div>

                        <div class="row">
                            <div class="col-md-6 mb-3">
                                <div class="form-group">
                                    <label class="mb-1 fw-bold">Email address</label>
                                    <input
                                        type="email"
                                        v-model="user.email"
                                        class="form-control"
                                        placeholder="Email Address"
                                    />
                                </div>
                            </div>
                            <div class="col-md-6 mb-3">
                                <div class="form-group">
                                    <label class="mb-1 fw-bold">Password</label>
                                    <input
                                        type="password"
                                        v-model="user.password"
                                        class="form-control"
                                        placeholder="Password"
                                    />
                                </div>
                            </div>
                            <div class="col-md-12 mb-3">
                                <div class="form-group">
                                    <label class="mb-1 fw-bold">Confirm Password</label>
                                    <input
                                        type="password"
                                        v-model="user.password_confirmation"
                                        class="form-control"
                                        placeholder="Confirm Password"
                                    />
                                </div>
                            </div>
                        </div>
                        <button type="submit" class="btn btn-primary w-100">REGISTER</button>
                    </form>
                </div>
            </div>
        </div>
    </div>
</template>
