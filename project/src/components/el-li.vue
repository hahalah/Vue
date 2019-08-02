<template>
    <div>
        <ul>
            <li class="title" @click="list.open=!list.open">
                <span>{{list.name}}</span>
                <div :style="{'display':list.open===true?'block':'none'}">
                    <span style="color:green" @click="add">添加</span>
                    <span style="color:red" @click="del(list.id)">删除</span>
                    <span style="color:orange" @click="change">修改</span>
                </div>
            </li>
            
           <li :style="{'display':list.open===true?'block':'none'}" v-for="(result,index) in list.children" :key="index">
               <El :list='result'></El>
           </li>
        </ul>
    </div>
</template>
<script>
export default {
    name:'El',
    props:['list'],
    methods:{
        add(){
            let name=prompt("请输入名字")
            let num=102
            if(this.list.children){
                this.list.children.push({
                id:num++,
                open:false,
                name:name
                })
            }else{
                let arr=[]
                arr.push({
                id:num++,
                open:false,
                name:name
                })
                this.list.children=arr
            }
            
        },
        del(id){
        let _this=this
        let ind=_this.$parent.list.findIndex((item)=>item.id===id)
        _this.$parent.list.splice(ind,1)
        },
        change(){
            let changeName=prompt("请输入要修改的名字")
            this.list.name=changeName
        }
    }
}
</script>

<style>
li{
    list-style: none;
}
.title{
    display: flex;
}
.title div{
    margin-left:15px;
}
</style>
