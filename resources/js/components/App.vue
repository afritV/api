<template>
<div>
    <nav class="navbar navbar-expand-lg navbar-light bg-light text-center">
            <div class="container">
                <ul class="navbar-nav">
                    <li class="nav-item">
                        <router-link class="nav-link" :to="{name:'home'}">Home</router-link>
                    </li>
                    <li class="nav-item">
                        <router-link class="nav-link" :to="{name:'desks'}">Desks</router-link>
                    </li>

                </ul>
            </div>
    </nav>
    <div>
        <router-view></router-view>

    </div>
</div>
</template>

<script>
export default {

}
</script>

