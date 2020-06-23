<template>
    <div>
        <b-navbar type="dark" variant="dark" class="mb-3">
            <b-navbar-brand>
                Elements
            </b-navbar-brand>
            <b-navbar-nav>
                <b-nav-item href="#">Home</b-nav-item>
                    <b-nav-item-dropdown text="User" right>
                        <b-dropdown-item href="#">Account</b-dropdown-item>
                        <b-dropdown-item href="#">Settings</b-dropdown-item>
                    </b-nav-item-dropdown>

                    <b-nav-item-dropdown text="Categorías" right>
                        <b-dropdown-item 
                            v-for="c in categories" 
                            v-bind:key="c.id" 
                            :to="'/category/' + c.id + '/element'">
                            {{ c.title}}
                        </b-dropdown-item>
                    </b-nav-item-dropdown>

                    <b-nav-item-dropdown text="Tipos" right>
                        <b-dropdown-item 
                            v-for="t in types" 
                            v-bind:key="t.id" 
                            :to="'/type/' + t.id + '/element'">
                            {{ t.title}}
                        </b-dropdown-item>
                    </b-nav-item-dropdown>
            </b-navbar-nav>
        </b-navbar>
    </div>
</template>

<script>
export default {

    created(){
        this.findAllCategory();
        this.findAllType();
    },

    data(){
        return{
            categories:[],
            types:[]

        };
    },
    methods: {
        findAllCategory: function(){
            fetch('http://127.0.0.1:8000/api/Category/?format=json')
                .then(res => res.json())
                //.then(res => console.log(res[0].id))
                .then(res => this.categories =res)
        },
        findAllType: function(){
            fetch('http://127.0.0.1:8000/api/Type/?format=json')
                .then(res => res.json())
                //.then(res => console.log(res[0].id))
                .then(res => this.types =res)
        }
    },
}
</script>