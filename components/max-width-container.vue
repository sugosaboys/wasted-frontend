<template>
    <div class="wrapper-container">
        <div class="container">
            <slot></slot>
        </div>
    </div>
</template>

<style scoped>
    .container{
        max-width: 1560px;
    }

    @media screen and (min-width:1560px){     
        .wrapper-container{
            display: grid;
            place-content: center;
        }
    }
</style>