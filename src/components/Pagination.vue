<template>
    <div class="pagination">
        <button @click="changeBtn">首页</button>
        <button @click="changeBtn">上一页</button>
        <button v-if="jduge" class="pagebtn">......</button>
        <!-- 页码按钮被点击时 -->
        <button v-for="btn in pagebtns" @click="changeBtn(btn)"
            :class="[{ currentPage: btn == currentPage }, 'pagebtn']">
            {{ btn }}
        </button>
        <button @click="changeBtn">下一页</button>
    </div>
</template>
<script>
import $ from 'jquery'
export default {
    name: 'Pagination',
    data() {
        return {
            pagebtns: [1, 2, 3, 4, 5, '......'],
            currentPage: 1,
            jduge: false
        }
    },
    methods: {
        changeBtn(page) {
            if (page === '......') {
                return;
            }
            //如果形参page不为number类型则判断按钮为首页按钮，上一页按钮，下一页按钮
            if (typeof page != 'number') {

                //通过按钮组件文本内容进行判断
                switch (page.target.innerText) {
                    case '上一页':
                        //触发当前页码按钮的上一个页码的按钮点击事件
                        $('button.currentPage').prev().click();
                        break;
                    case '下一页':
                        //触发当前页码按钮的下一个页码的按钮点击事件
                        $('button.currentPage').next().click();
                        break;
                    case '首页':
                        //重置pagebtns
                        this.pagebtns = [1, 2, 3, 4, 5, '.....'];
                        //并调用changeBtn函数并传值1，使其跳转到页码为1的首页
                        this.changeBtn(1);
                        break;
                    default:
                        break;
                }
                return;

            }
            this.currentPage = page;
            //当当前页面数量大于4的时候
            if (page > 4) {
                //显示页码省略按钮
                this.jduge = true;
            } else {
                this.jduge = false;
            }
            if (page == this.pagebtns[4]) {
                this.pagebtns.shift();//移除第一个元素
                this.pagebtns.splice(4, 0, this.pagebtns[3] + 1);//添加往数列末端添加一个页码元素，该页码元素为倒数第二个页码按钮的页码基础上再加1
            } else if (page == this.pagebtns[0] && page != 1) {
                //先在第一个位置加一个页码元素，该页码元素为正数第二个页码按钮的页码基础上再加1
                this.pagebtns.unshift(this.pagebtns[0] - 1);
                //移除最后一个数字
                this.pagebtns.splice(5, 1);
            }
            //触发并将当前页码传参给handleList事件，
            this.$emit('handleList', this.currentPage);
        }
    }
}
</script>
<style scoped>
.pageination {
    margin-top: 5px;
    margin-bottom: 20px;
    background-color: white;
    padding: 6px 20px;
    border-radius: 5px;
    border: 1px solid #888888;
}

button {
    background-color: #fff;
    border: 1px solid #ddd;
    color: #778087;
    border-radius: 3px;
    outline: none;
    height: 21px;
    cursor: pointer;
    padding: 0 2px;
    width: 55px;
    height: 29px;
}

.pagebtn {
    position: relative;
    bottom: 1px;
    width: 40px;
    margin: 0 4px;
}

.currentPage {
    color: white;
    background-color: #1f1b1b;

}
</style>