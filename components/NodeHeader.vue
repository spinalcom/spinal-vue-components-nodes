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
    <div class="node-header"
         @click="$emit('node-selected', [nodeId])">

        <drop-up-down-button
                class="node-list-icon"
                @click="$emit('toggle-display-child')"
                :style="{visibility: isVisible}"/>

        <div class="node-name">
            {{name}}
        </div>

        <i class="material-icons node-hide-bim"
           @click="hideBimObj()"
           v-if="showHideObject"
        >
            remove_red_eye
        </i>

        <color-marker
                class="node-color"
                :color="color"
        />

    </div>
</template>

<script>
    import DropUpDownButton from "spinal-vue-components-buttons";
    import {ColorMarker} from "spinal-vue-components-color-markers";

    export default {
        name: "NodeHeader",
        components: {ColorMarker, DropUpDownButton},
        props: {

            hasChild: {
                type: Boolean,
                required: true
            },

            name: {
                type: String,
                required: true
            },

            nodeId: {
                type: String,
                required: true
            },

            color: {
                type: String,
                default: function() {
                    return ""
                }
            },
            showHideObject: {
                type: Boolean,
                default: function () {
                    return false
                }
            }

        },

        computed: {
            isVisible: function() {
                return this.hasChild ? "" : "hidden";
            }
        },

        watch: {
            hasChild: {
                handler: function (oldValue, newValue) {
                    if (typeof newValue === "undefined") {
                        if (typeof oldValue !== "undefined" && !oldValue)
                            this.isVisible = "hidden"

                    }
                    else if (!newValue) {
                        this.isVisible = "hidden";
                    }
                    else {
                        this.isVisible = "";
                    }
                },
                immediate: true
            }
        },

        methods: {
            hideBimObj: function () {
                this.$emit('hide-bim-object', [this.nodeId]);
            }
        }
    }
</script>

<style scoped>

    .node-header {
        position: relative;
        width: 100%;
        height: 36px;
        padding: 9px 6px 6px 13px;
    }

    .node-header:hover {
        background-color: rgba(0, 0, 0, 0.3);
        cursor: pointer;
    }

    .node-list-icon {
        position: absolute;
        left: 0;
        top: 7px;
        width: 21px;
    }

    .node-name {
        position: absolute;
        left: 26px;
        white-space: nowrap;
        overflow: hidden;
        text-overflow: ellipsis;
        width: calc(100% - 77px);
    }

    .node-hide-bim {
        position: absolute;
        right: 15px;
        top: 6px;
    }

    .node-color {
        position: absolute;
        right: 0;
    }


</style>