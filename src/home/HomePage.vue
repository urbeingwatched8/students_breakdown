<template>
    <div>
        <h1>Hi {{account.user.firstName}}!</h1>
        <p>Surname: {{account.user.lastName}}</p>
        <p>Email: {{account.user.username}}</p>
        <!--<h3>Users from secure api end point:</h3>-->
        <!--<em v-if="users.loading">Loading users...</em>-->
        <!--<span class="text-danger" v-if="users.error">ERROR: {{users.error}}</span>-->
        <!--<ul v-if="users.items">-->
        <p :key="user.id" v-for="user in users.items">
            <!--{{user.firstName + ' ' + user.lastName}}-->
            <span v-if="user.deleting"><em>Delete user</em></span>
                <span class="text-danger" v-else-if="user.deleteError"> - ERROR: {{user.deleteError}}</span>
            <span v-else> <a @click="deleteUser(user.id)" class="text-danger">Delete myself</a></span>
        </p>
        <!--</ul>-->
        <p>
            <router-link to="/login">Logout</router-link>
        </p>
    </div>
</template>

<script>
    import {mapActions, mapState} from 'vuex'

    export default {
        computed: {
            ...mapState({
                account: state => state.account,
                users: state => state.users.all
            })
        },
        created() {
            this.getAllUsers();
        },
        methods: {
            ...mapActions('users', {
                getAllUsers: 'getAll',
                deleteUser: 'delete'
            })
        }
    };
</script>