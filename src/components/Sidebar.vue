<template>
    <div>
        <template v-if="item.children">
            <el-submenu v-if="!(item.path!=''&&item.path!=' '&&item.path!='-')" :index="item.id+'index'" :key="item.path" >
                <template slot="title" >
                    <i v-if="item.children&&item.children.length>0&&item.iconCls" class="fa" :class="item.iconCls"></i>
                    <span class="title-name" slot="title">{{item.name}}</span>
                </template>
                <template v-for="child in item.children">
                    <!-- 这里实现自己递归嵌套 -->
                    <template v-if="!child.IsHide">
                        <sidebar
                                v-if="child.children&&child.children.length>0"
                                :item="child"
                                :index="child.id"
                                :key="child.path"/>
                        <el-menu-item v-else :key="child.path" :index="child.path">
                            <i v-if="child.children&&child.children.length>0&&item.iconCls" :class="item.iconCls"></i>
                            {{child.name}}
                        </el-menu-item>
                    </template>
                </template>
            </el-submenu>
            <template v-else>
                <el-menu-item :index="item.path" :key="item.path+'d'">
                    <i class="fa" :class="item.iconCls"></i>
                    <template slot="title">
                        <span class="title-name" slot="title">{{item.name}}</span>
                    </template>
                </el-menu-item>
            </template>
        </template>
        <!-- 没有子节点，直接输出 -->
        <template v-else>
            <el-menu-item :index="item.path" :key="item.path+'d'">
                <i class="fa" :class="item.iconCls"></i>
                <template slot="title">
                    <span class="title-name" slot="title">{{item.name}}</span>
                </template>
            </el-menu-item>
        </template>
    </div>
</template>

<script>
    export default {
        name: 'Sidebar',
        props: {
            item: {
                type: Object,
                required: true
            }
        }
    }
</script>
