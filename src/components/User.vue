<template>
  <div class="user" v-if="user">
    <div class="user__left">
        <img :src="user.avatar_url" alt="">
        <a :href="user.html_url" class="user__left-btn">ПОСЕТИТЬ</a>
    </div>
    <div class="user__right">
        <p>{{ user.login }}</p>
        <p>Репозиториев: <span>{{ user.public_repos }}</span> </p>
        <p>Создан: <span>{{ user.created_at }}</span></p>
        <p>Подписщиков:  <span>{{ user.followers }}</span></p>
        <p>Подписок: <span>{{ user.following }}</span></p>
    </div>
  </div>
  <div class="sort">
    <h2 class="sort__title">Сортировка</h2>
    <div class="sort__box">
        <button 
            class="sort__box-btn " 
            v-for="(btn, index) in btns"
            :key="btn.name"
            :class="{active: isActive == index}"
            @click="SortRepos(index, btn.sortType)"
        >
            {{ btn.name }}
        </button>
    </div>
  </div>
</template>

<script>

import { mapState, mapMutations } from 'vuex'

export default {
    computed: {
        ...mapState([['user']])
    },
    data() {
        return {
            isActive: 0,
            btns: [
                { name: 'ИМЯ', sortType: 'name'},
                { name: 'ЗВЕЗДЫ', sortType: 'stargazers_count'},
                { name: 'ДАТА', sortType: 'created_at'}
            ]
        }
    },
    methods: {
        ...mapMutations(['sort']),
        SortRepos(index, sortType) {
            this.isActive = index
            this.sort(sortType)
        }
    }
}
</script>

<style>

</style>