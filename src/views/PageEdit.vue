<template>
    <h4>Editar {{ page.pageTitle }}</h4>

    <form action="" class="container mb-3">
        <div class="row">
            <div class="col-md-8">
                <div class="mb-3">
                    <label for="" class="form-label">
                        Título da Página
                    </label>
                    <input 
                        type="text"
                        class="form-control"
                        v-model="page.pageTitle"
                    >
                </div>
                <div class="mb-3">
                    <label for="" clas="form-label">
                        Conteúdo
                    </label>
                    <textarea
                        type="text"
                        class="form-control"
                        rows="5"
                        v-model="page.content"
                    ></textarea>
                </div>
            </div>
            <div class="col">
                <div class="mb-3">
                    <label for="" class="form-label">
                        Texto de Link
                    </label>
                    <input 
                        type="text"
                        class="form-control"
                        v-model="page.link.text"
                    >
                </div>
                <div class="row mb-3">
                    <div class="form-check">
                        <input 
                        class="form-check-input"
                        type="checkbox"
                        v-model="page.published"
                        >
                        <label class="form-check-label" for="gridCheck1">
                            Publicado
                        </label>
                    </div>
                </div>
            </div>
        </div>

        <div class="mb-3">
            <button
                class="btn btn-primary me-2"
                @click.prevent="submit"
            >Editar</button>
            <button
                class="btn btn-secondary me-2"
                @click.prevent="goToPagesList"
            >Cancelar</button>
            <button
                class="btn btn-danger"
                @click.prevent="deletePage"
            >Deletar</button>
        </div>
    </form>
</template>

<script setup>
import { useRouter } from 'vue-router';
import { inject } from 'vue';

const router = useRouter();
const pages = inject('$pages');
const bus = inject('$bus');

const {index} = defineProps(['index']);

let page = pages.getSinglePage(index);

function submit() {
    pages.editPage(index, page);

    bus.$emit('page-updated', {
        index,
        page
    });

    goToPagesList();
}

function deletePage() {
    pages.removePage(index);

    bus.$emit('page-deleted', {index});

    goToPagesList();
}

function goToPagesList() {
    router.push({path: '/pages'}) 
}

</script>