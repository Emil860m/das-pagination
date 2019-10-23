<template>
    <div align="center" v-if="pages.length > 1" :onload="emitToParent()">
        <p style="font-size: smaller; left: 50%">Page {{ page }} of {{ pages.length}}</p>
        <ul class="pagination">
            <li class="page-item">
                <button type="button" class="page-link" :disabled="page === 1" @click="previousPage()"> Previous </button>
            </li>
            <li class="page-item">
                <button type="button" v-bind:key="pageNumber" class="page-link" v-for="pageNumber in pages" :disabled="page === pageNumber" @click="selectPage(pageNumber)"> {{pageNumber}} </button>
            </li>
            <li class="page-item">
                <button type="button" @click="nextPage()" :disabled="page === pages.length" class="page-link"> Next </button>
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    name: 'Pagination',
    props: {
        perPage: {
            type: Number,
            default: 8
        },
        items: {
            type: Array,
            default: function () { return [] }
        }
    },
    data () {
        return {
            page: 1,
            pages: []
        }
    },
    methods: {
        paginate (posts) {
            let page = this.page
            let perPage = this.perPage
            let from = (page * perPage) - perPage
            let to = page * perPage
            return posts.slice(from, to)
        },
        setPages () {
            this.pages.length = 0
            let numberOfPages = Math.ceil(this.items.length / this.perPage)
            for (let index = 1; index <= numberOfPages; index++) {
                this.pages.push(index)
            }
            if (this.page > this.pages.length) this.page = 1
        },
        emitToParent () {
            this.$emit('paginate', this.paginate(this.items))
        },
        previousPage () {
            this.page--
        },
        nextPage () {
            this.page++
        },
        selectPage (pageNumber) {
            this.page = pageNumber
        }
    },
    watch: {
        items () {
            this.setPages()
        }
    }
}
</script>

<style>
.pagination {
    margin: 0 !important;
}
button.page-link {
    background-color: #1b1b1b;
    color: white;
    border-radius: 15px;
    display: inline-block;
    padding: 7px 16px;
    text-align: center;
    text-decoration: none;
}
button:disabled {
    background-color: #5e5e5e !important;
}
</style>
