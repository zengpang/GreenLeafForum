<template>
    <div class="pagination">
        <button @click="changeBtn">首页</button>
        <button @click="changeBtn">上一页</button>
        <button v-if="jduge" class="pagebtn">......</button>
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
            //如果形参page不为number类型则判断按钮为首页按钮，上一页按钮，下一页按钮
            if (typeof page != 'number') {
                try {
                    //通过按钮组件文本内容进行判断
                    switch (page.target.innerText) {
                        case '上一页':
                            $('button.currentPage').prev().click();
                            break;
                        case '下一页':
                            $('button.currentPage').next().click();
                            break;
                        case '首页':
                            this.pagebtns = [1, 2, 3, 4, 5, '.....'];
                            this.changeBtn(1);
                            break;
                        default:
                            break;
                    }
                    return;
                } catch (ex) {
                    return;
                } 
            }
            this.currentPage = page;
            //当页面数量大于4的时候
            if (page > 4) {
                //显示页码省略按钮
                this.jduge = true;
            } else {
                this.jduge = false;
            }
            if (page == this.pagebtns[4]) {
                this.pagebtns.shift();//移除第一个元素
                this.pagebtns.splice(4, 0, this.pagebtns[3] + 1);//添加最后一个
            } else if (page == this.pagebtns[0] && page != 1) {
                //先在第一个位置加一个
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