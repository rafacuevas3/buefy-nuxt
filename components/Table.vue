<template>
    <div class="container">
        <section>
            <b-progress type="is-info" size="is-small" v-show="loading"></b-progress>

            <b-table
                :data="data"
                :loading="loading"

                paginated
                pagination-position="top"
                backend-pagination
                :total="total"
                :per-page="perPage"
                @page-change="onPageChange"
                aria-next-label="Next page"
                aria-previous-label="Previous page"
                aria-page-label="Page"
                aria-current-label="Current page"

                backend-sorting
                :default-sort-direction="defaultSortOrder"
                :default-sort="[sortField, sortOrder]"
                @sort="onSort">

                <b-table-column field="original_title" label="Title" sortable v-slot="props">
                    {{ props.row.original_title }}
                </b-table-column>

                <b-table-column field="vote_average" label="Vote Average" numeric sortable v-slot="props">
                    <span class="tag" :class="type(props.row.vote_average)">
                        {{ props.row.vote_average }}
                    </span>
                </b-table-column>

                <b-table-column field="vote_count" label="Vote Count" numeric sortable v-slot="props">
                        {{ props.row.vote_count }}
                </b-table-column>

                <b-table-column field="release_date" label="Release Date" sortable centered v-slot="props">
                    {{ props.row.release_date | dateFormat }}
                </b-table-column>

                <b-table-column label="Overview" width="500" v-slot="props">
                    {{ props.row.overview | truncate(80) }}
                </b-table-column>

            </b-table>
        </section>
    </div>
</template>

<script>
    export default {
        filters: {
            truncate(text, limit) {
                return text.length > limit ? text.substring(0, limit) + '...' : text;
            },
            dateFormat(date) {
                return date ? (new Date(date)).toLocaleDateString('en-US', { day: '2-digit', month: 'long', year: 'numeric' }) : 'unknow';
            }
        },
        data() {
            return {
                data: [],
                total: 0,
                loading: false,
                sortField: 'vote_count',
                sortOrder: 'desc',
                defaultSortOrder: 'desc',
                page: 1,
                perPage: 20
            }
        },
        methods: {
            onSort(field, order) {
                this.sortField = field
                this.sortOrder = order
                this.loadAsyncData()
            },
            onPageChange(page) {
                console.log(page)
                this.page = page;
                
                this.loadAsyncData(this.sortingPriority)
            },
            type(value) {
                const number = parseFloat(value)
                if (number < 6) {
                    return 'is-danger'
                } else if (number >= 6 && number < 8) {
                    return 'is-warning'
                } else if (number >= 8) {
                    return 'is-success'
                }
            },
            loadAsyncData(sortingPriority = []) {
                const params = [
                    'api_key=bb6f51bef07465653c3e553d6ab161a8',
                    'language=en-US',
                    'include_adult=false',
                    'include_video=false',
                    `sort_by=${this.sortField}.${this.sortOrder}`,
                    `page=${this.page}`
                ].join('&')
                
                this.loading = true

                this.$axios.get(`https://api.themoviedb.org/3/discover/movie?${params}`).then(({ data }) => {
                    this.data = []
                    
                    let currentTotal = data.total_results
                    
                    if (data.total_results / this.perPage > 1000) {
                        currentTotal = this.perPage * 1000
                    }
                    
                    this.total = currentTotal
                    
                    data.results.forEach((item) => {
                        item.release_date = item.release_date ? item.release_date.replace(/-/g, '/') : null
                        
                        this.data.push(item)
                    })
                    
                    this.loading = false
                })
                .catch((error) => {
                    this.data = []
                    this.total = 0
                    this.loading = false
                    throw error
                });
            }
        },
        created() {

            this.loadAsyncData([]);
        }
    }
</script>
