<template>
    <nav class="main-header navbar navbar-expand navbar-white navbar-light">
        <!-- Left navbar links -->
        <ul class="navbar-nav">
            <li class="nav-item">
                <a class="nav-link" data-widget="pushmenu" href="#" role="button"><i class="fas fa-bars"></i></a>
            </li>
        </ul>

        <!-- Right navbar links -->
        <ul class="navbar-nav ml-auto">
            <li class="nav-item">
                <a class="nav-link" data-widget="fullscreen" href="#" role="button">
                    <i class="fas fa-expand-arrows-alt"></i>
                </a>
            </li>

            <li class="nav-item">
                <a @click="signOut" class="nav-link" role="button">
                    <i class="fas fa-sign-out-alt text-danger"></i>
                </a>
            </li>
        </ul>
    </nav>
</template>

<script setup>
import { useRouter } from 'vue-router';
import Swal from 'sweetalert2';
import { apiSignOut } from '@/functions/api/auth';
import { useUserStore } from '@/stores/user';

const router = useRouter();
const userStore = useUserStore();

async function signOut() {
    const result = await Swal.fire({
        title: 'Sign Out?',
        text: 'You will be signed out from the system!',
        icon: 'warning',
        showCancelButton: true,
        confirmButtonColor: '#3085d6',
        cancelButtonColor: '#d33',
        confirmButtonText: 'Yes, sign me out!'
    });

    if (!result.isConfirmed) return;

    const token = userStore.getSanctumToken();
    try {
        await apiSignOut(token);
    } catch (e) {
        // ignore API errors and proceed to clear local state
    } finally {
        userStore.reset();
        router.replace({ name: 'SignIn' });
    }
}
</script>