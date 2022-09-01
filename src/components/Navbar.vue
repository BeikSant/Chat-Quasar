<script setup>
import { GoogleAuthProvider, signInWithPopup, signOut } from "firebase/auth";
import { auth } from "../firebase";
import { ref , inject } from 'vue'

const rightDrawerOpen = ref(false)
const userGoogle = inject("userGoogle");


const toggleRightDrawer = () => {
    rightDrawerOpen.value = !rightDrawerOpen.value
};

const accessGoogle = () => {
    const provider = new GoogleAuthProvider();
    signInWithPopup(auth, provider)
        .catch(error => console.log(error));
};

const logoutGoogle = () => {
    signOut(auth)
        .catch(error => console.log(error));
};


</script>

<template>
    <q-header elevated class="bg-primary text-white" height-hint="98">
        <q-toolbar>
            <q-toolbar-title>
                <q-avatar>
                    <img src="https://cdn.quasar.dev/logo-v2/svg/logo-mono-white.svg">
                </q-avatar>
                Quasar Chat
            </q-toolbar-title>

            <q-btn label="Ingresar" color="positive" @click="accessGoogle" v-if="!userGoogle"></q-btn>
            <q-btn label="Salir" color="negative" @click="logoutGoogle" v-if="userGoogle"></q-btn>
            <q-btn dense flat round icon="menu" @click="toggleRightDrawer" v-if="userGoogle" />
        </q-toolbar>

        <q-tabs align="left">

            <q-route-tab to="/page1" label="Page One" />
            <q-route-tab to="/page2" label="Page Two" />
            <q-route-tab to="/page3" label="Page Three" />
        </q-tabs>
    </q-header>

    <q-drawer show-if-above v-model="rightDrawerOpen" side="right" elevated>
        <!-- drawer content -->
    </q-drawer>

</template>