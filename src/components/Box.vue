<template>
   <div class="box has-text-wight-bold" :style="estilos">
       <slot>
        
        </slot>
    </div> 
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
    name: 'BoxItem',
    data () {
        return {
            estilos: {
                //'background-color': "#FAF0CA"
                // backgorunColor : "#FAF0CA"
                background: '#FAF0CA'
            }
        }
    }        
})
</script>