<template>
    <form action="" class="container mb-3">
        <div class="row">
            <div class="col-md-8">
                <div class="mb-3">
                    <label for="" class="form-label">
                        Nome da Página
                    </label>
                    <input
                        type="text"
                        class="form-control"
                        v-model="pageTitle"
                    />
                </div>
                <div class="mb-3">
                    <label for="" class="form-label">
                        Conteúdo
                    </label>
                    <textarea
                        type="text"
                        class="form-control"
                        rows="5"
                        v-model="content"
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
                        v-model="linkText"
                    />
                </div>
                <div class="row mb-3">
                    <div class="form-check">
                        <input class="form-check-input" type="checkbox" v-model="published">
                        <label class="form-check-label" for="gridCheck1">
                        Publicado
                        </label>
                    </div>
                </div>
            </div>
        </div>
            <div class="mb-3">
                <button
                    class="btn btn-primary"
                    :disabled="isFormInvalid"
                    @click.prevent="submitForm"
                >Criar Página</button>
            </div>
        </form>
</template>
<script setup>  
import {inject, ref, computed, watch} from 'vue';
import {useRouter} from 'vue-router'

const bus = inject('$bus')
const pages = inject('$pages');
const router = useRouter();

let pageTitle = ref('');
let content = ref('');
let linkText = ref('');
let linkUrl = ref('');
let published = ref(true);

function submitForm() {
    if (!pageTitle || !content || !linkText) {
        alert ('Favor preencher todo o formulário.');
        return;
    }
    let newPage = {
        pageTitle: pageTitle.value,
        content: pageTitle.value,
        link: {
            text: linkText.value,
        },
        published: pageTitle.value
    }
    
    pages.addPage(newPage)

    bus.$emit('page-created', newPage);

    router.push({path: '/pages'});
}

const isFormInvalid = computed(() => !pageTitle || !content || !linkText || !linkUrl);

watch(pageTitle, (newTitle, oldTitle) => {
    if (linkText.value === oldTitle) {
        linkText.value = newTitle;
    }
})
    
</script>
