<template>
    <div class="center">
        <h3 class="lobster">{{ $t("home.welcome_msg") }}<sup>{{current_version}}</sup></h3>
        <p>{{ $t("home.help_msg") }}</p>
        <button class="btn btn-primary" v-on:click="next()">{{ $t("home.start_btn") }}</button>
    </div>
</template>

<script>
import router from '../router'

export default {
    name: 'home',
    props: { saved_ssid: String, list_ssids: Array, internet: Boolean },
     data() {
        return {
            current_version:"" 
        }
    },
    methods: {
        next: function() {
            var saved_ssid = this.saved_ssid
            var list_ssids = this.list_ssids
            var internet = this.internet
            if (window.config.iface_out.charAt(0) == 'e'){
                router.push({ name: 'generate-ap' });
            } else if (!window.config.choose_net && this.internet){
                router.push({ name: 'generate-ap' });
            } else {
                router.push({ name: 'wifi-select', 
                              params: { saved_ssid: saved_ssid, 
                                        list_ssids: list_ssids, 
                                        internet: internet } });
            }
        }
    },
    created: function() {
        if ('current_version' in window)
            this.current_version = window.current_version
    }
}
</script>
