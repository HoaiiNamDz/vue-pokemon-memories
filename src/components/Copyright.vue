<template>
    <div class="copyright">
        <div class="container">
            <p class="text">This game owned by NHN</p>
            <a href="https://github.com/HoaiiNamDz" class="icon">
                <i class="fa-brands fa-github"></i>
            </a>
        </div>
    </div>
</template>
<script>
export default {
    
}
</script>
<style scoped>
    .copyright {
        font-size: 18px;
        z-index: 2;
        position: fixed;
        bottom: 0;
        left: 0;
        right: 0;
        color: var(--light);
    }
    .container {
        display: flex;
        justify-content: center;
    }
    .icon {
        color: var(--light);
        margin: 0 4px;
    }
</style>