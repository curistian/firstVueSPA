<template>
    <li>
        <router-link
            :to="`/${index}`"
            class="nav-link"
            active-class="active emphasize"
            aria-current="page"
            :title="`esse link vai para a página de ${page.link.text}`"
        >{{page.link.text}}</router-link>
    </li>
</template>

<script>
export default {
    props: ['page', 'index']
}
</script>
