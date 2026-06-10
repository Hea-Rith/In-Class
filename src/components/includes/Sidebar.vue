<template>
    <aside class="main-sidebar sidebar-dark-primary elevation-4">
        <!-- Brand Logo -->
        <div class="brand-section position-relative">
            <a href="#" class="brand-link d-flex align-items-center" @click.prevent="toggleUserMenu">
                <img :src="logoImage" alt="Chat System Logo" class="brand-image img-circle elevation-3" style="opacity: .8">
                <span class="brand-text font-weight-light ml-2">Chat System</span>
            </a>
            <div v-if="menuOpen" class="dropdown-menu show position-absolute" style="top: 100%; left: 0; width: 100%; z-index: 1000;">
                <button type="button" class="dropdown-item w-100 text-left" @click="signOut">
                    <i class="fas fa-sign-out-alt mr-2"></i>
                    Sign Out
                </button>
            </div>
        </div>

        <!-- Sidebar -->
        <div class="sidebar">
            <!-- Sidebar user panel (optional) -->
            <div class="user-panel mt-3 pb-3 mb-3 d-flex">
                <div class="image">
                    <img :src="emptyImage" class="img-circle elevation-2" alt="User Image">
                </div>
                <div class="info">
                    <a href="#" class="d-block">Alexander Pierce</a>
                </div>
            </div>

            <!-- Sidebar Menu -->
            <nav class="mt-2">
                <ul class="nav nav-pills nav-sidebar flex-column" data-widget="treeview" role="menu"
                    data-accordion="false">
                    <li class="nav-item">
                        <RouterLink :to="{ name: 'Dashboard' }" active-class="active" class="nav-link">
                            <i class="nav-icon fas fa-tachometer-alt"></i>
                            <p>
                                Dashboard
                            </p>
                        </RouterLink>
                    </li>
                </ul>
            </nav>
            <!-- /.sidebar-menu -->
        </div>
        <!-- /.sidebar -->
    </aside>
</template>

<script setup>
import { ref } from 'vue';
import { useRouter } from 'vue-router';
import logoImage from '@/assets/images/logoImage.svg';
import emptyImage from '@/assets/images/emptyImage.svg';

const router = useRouter();
const menuOpen = ref(false);

function toggleUserMenu() {
    menuOpen.value = !menuOpen.value;
}

function signOut() {
    menuOpen.value = false;
    router.replace({ name: 'SignIn' });
}
</script>