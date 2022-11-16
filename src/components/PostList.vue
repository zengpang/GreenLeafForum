<template>
    <div class="PostList">
        <!--在数据未返回的时候，显示这个正在加载的gif-->
        <div class="loading" v-if="isLoading">
            <img src="../assets/loading.gif">
        </div>
        <div class="posts" v-else>
            <ul>
                <li>
                    <div class="toobar">
                        <span>全部</span>
                        <span>精华</span>
                        <span>分享</span>
                        <span>问答</span>
                        <span>招聘</span>
                    </div>
                </li>
                
            </ul>
        </div>
    </div>
</template>
<script>
import pagination from './Pagination'
export default {
    name: 'PostList',
    data() {
        return {
            isLoading: false,
            posts: [],//代表页面的列表数组
            postpage: 1
        }
    },
    components: {
        pagination
    },
    methods: {

    }
}
</script>