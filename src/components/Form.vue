<template>
    <form :action="action" >
        <template v-for="(field, index) in fields" >
            <div class="form-group" :key="index" >
                <input :ref="field.name" class="form-control" :class="field.classes" :type="field.type" v-model="field.value" :placeholder="field.hint" v-if="field.type !== 'textArea'" >
                <textarea :ref="field.name" class="form-control" v-model="field.value" :placeholder="field.hint" v-else ></textarea>
            </div>
        </template>

        <div class="form-group" >
            <button type="button" class="btn" @click="showUser" >
                <template v-if="submitText" >{{submitText}}</template>
                <template v-else >Submit</template>
            </button>
        </div>
    </form>
</template>


<script>
    export default {
        name: 'Form',
        props: {
            action: String,
            fields: Array,
            submitText: String,
        },
        computed: {
            user() {
                let user = {};
                this.fields.forEach((item) => {
                    user[item.name] = item.value;
                });

                return user;
            },
        },
        methods: {
            showUser: function () {
                this.$store.commit('addUser', this.user);
            },
        }
    }
</script>

<style scoped>
    form {
        padding: 1rem;
    }

    .form-group {
        margin-bottom: 1.25rem;
    }

    .form-control {
        border: none;
        outline: none;
        border-bottom: 1px solid #5c5c5c;
        padding: 1rem 0.25rem;
        letter-spacing: 1px;
        min-width: 20rem;
    }
</style>