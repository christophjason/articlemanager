<template>
    <nav class="navbar navbar-expand-sm navbar-dark bg-dark mb-2">
        <div class="container">
            <a href="#" class="navbar-brand">Article Manager</a>
            <form @submit.prevent="searchArticle" class="form-inline">
                <input class="form-control mr-sm-2" type="search" placeholder="Search"
                       v-model="searchQuery" aria-label="Search">
                <button class="btn btn-outline-success my-2 my-sm-0" type="submit">Search</button>
            </form>
        </div>
    </nav>
</template>

<script>
    export default {
        data() {
            return {
                articles: [],
                article: {
                    id: '',
                    title: '',
                    body: ''
                },
                article_id: '',
                pagination: {},
                edit: false
            }
        },

        methods: {
            searchArticle(searchQuery) {
                //Search
                fetch('api/article', {
                    method: 'get',
                    body: JSON.stringify(this.article),
                    headers: {
                        'content-type': 'application/json'
                    }
                })
                    .then(res => res.json())
                    .then(data => {
                        this.article.title = '';
                        this.article.body = '';
                        this.fetchArticles();
                    })
                    .catch(err => console.log(err));
            }
        }

    }
</script>

<style scoped>

</style>