<script lang="ts">

export default{}
</script>

<template>

<footer class="footer">

<div class="year">© 2023</div>
<a href="https://github.com/PteNiX?tab=repositories" class="github"> by PteN</a>
<div class="version">beta version</div>


</footer>
</template>


<style scoped>
.footer{
    display: flex;
    flex-direction: row;
    color: white;
    justify-content: space-between;
    margin: auto;
    width: 90%;
    height: 3rem;
    align-items: center;

}
    .github{
        text-decoration: none;
        color: white;

    }

    .github:hover {
            color:rgb(255, 215, 0); 
        }

    .year{
        padding-left: 2rem;

    }
    .version{
        padding-right: 2rem;


    }

</style>


