<template>
    <div>
        <iv-modal :color="theme" :positionModal="positionData">

            <template #header>
                <div :style="modalHeader" class="iv-guidance-modal-header">
                    <div class="iv-guidance-modal-title">Select Guidance Branch</div>
                    <div @click="closeWindow" class="iv-guidance-modal-close-button" :style="modalCloseButton" >
                        <img class="iv-guidance-modal-closeImage"  src="./assets/close.svg" />
                    </div>
                </div>
            </template>

            <template  #body >
                <div class ="branchList" :style="modalBody">
                    <div class="iv-guidance-home-branch-button" v-for=" branch in guidanceInput" :key="branch.title" @click="handleBranch(branch.branch_data)" :style="modalBranch" >{{branch.title}}</div>
                </div>
            </template>

        </iv-modal> 
    </div>
</template>
<script>
import Guidance from "@/mixins/Guidance";
import guidanceBus from '@/buses/guidanceBus.js';
import Theme from '@/Theme.js'

export default {
    name:"iv-guidance-home",
    props:{
        guidanceInput:{
            type:Array,
        },
    },
    mixins:[Guidance],
    data(){
        return{
            theme: Theme.DeepBlue,
            positionData:["50%",null,null,"50%"],
        }
    },
    methods:{
        handleBranch(branchData){
            guidanceBus.$emit("select-branch", branchData);
        },
        closeWindow(){
            guidanceBus.$emit("close-window", this._uid);
        },
    },
    computed:{
        modalBranch(){
            return{
                backgroundColor: this.theme.dark,
            }
        },
    }
}
</script>
<style lang="scss">
@import "src/globals.scss";
.branchList{
    position:relative;
    min-height: 200px;
    max-height: 2vh;
    min-width: 400px;
    padding: 5px 5px 5px 5px;
    margin: 5px 5px 5px 5px;

    display: flex;
    flex-direction: column;
    justify-content: space-around;
    align-items: center;
}

.iv-guidance-home-branch-button{
    position:relative;

    width: 30%;
    padding: 5px 0px 5px 0px;
    //margin: auto;
    margin: 5px auto 5px auto;
    cursor: pointer;
    font-size: 20px;
    text-align: center;
    color: $white;
    background-color:$secondaryMediumGreen;
}

</style>