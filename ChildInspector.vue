<!--
  - /*
  -  * Copyright (c) 2018. SpinalCom - www.spinalcom.com
  -  *
  -  * This file is part of SpinalCore.
  -  *
  -  * Please read all of the following terms and conditions
  -  * of the Free Software license Agreement ("Agreement")
  -  * carefully.
  -  *
  -  * This Agreement is a legally binding contract between
  -  * the Licensee (as defined below) and SpinalCom that
  -  * sets forth the terms and conditions that govern your
  -  * use of the Program. By installing and/or using the
  -  * Program, you agree to abide by all the terms and
  -  * conditions stated or referenced herein.
  -  *
  -  * If you do not agree to abide by these terms and
  -  * conditions, do not demonstrate your acceptance and do
  -  * not install or use the Program.
  -  * You should have received a copy of the license along
  -  * with this file. If not, see
  -  * <http://resources.spinalcom.com/licenses.pdf>.
  -  */
  -->

<template>
    <div class="child-inspector">
        <div class="child-inspector-name">
            <h1>
                {{name}}
            </h1>
        </div>


        <div class="child-inspector-child"
             v-for="(info, index) in childInfo"
             :key="index">
            <div class="child-inspector-child-name">
                <h2>
                    {{info.name}}
                </h2>
            </div>


            <spinal-icon-button
                    class="child-inspector-delete-child"
                    icon="delete"
                    tool-tip="suppress child"
            />
        </div>


    </div>
</template>

<script>
    import NodeHeader from "./NodeHeader";
    import {SpinalIconButton} from "spinal-vue-components-buttons";

    export default {
        name: "ChildInspector",
        components: {SpinalIconButton, NodeHeader},
        props: {
            name: {
                type: String,
                required: true
            },
            childInfo: {
                type: Array,
                default: function () {
                    return [
                        {name: "child 1"},
                        {name: "child 2"},
                        {name: "child 3"},
                        {name: "child 4"}
                    ];
                }
            },
            defaultRelationName: {
                type: String,
                default: function () {
                    return ""
                }
            }
        },
        data: function () {
            return {
                relationName: "hah"
            }
        },
        mounted() {
            this.relationName = this.defaultRelationName;
        }

    }
</script>

<style scoped>

    .child-inspector-name {
        height: 30px;
    }

    .child-inspector-child-name {
        height: 55px;
    }

    .child-inspector-child {
        border: 1px solid #979797;
        position: relative;
        width: 100%;
        height: 55px;
    }

    .child-inspector-delete-child {
        position: absolute;
        right: 0;
        top: 5px;
    }


</style>