<template lang="">
    <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/addcontacts">Add Contacts</RouterLink>
    </nav>
</template>
<script>
export default {
    name: "Navbar",
}
</script>
<style>
    nav{
        background-color: #222;
        border-bottom: 4px solid #111;
        padding: 15px 50px;
        display: flex;
        justify-content: flex-end;
        align-items: center;
    }
    #logo-url{
        margin: auto;
        margin-left: 0;
    }
    nav a {
        color: #FCBA03;
        text-decoration: none;
        margin: 12px;
        transition: .5s;
    }
    nav a:hover{
        color: #fff;
    }
</style>