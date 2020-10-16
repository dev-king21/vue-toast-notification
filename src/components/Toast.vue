<template>
    <ul class="el-toast">
        <toast-item v-for="(toast, index) in toasts" :key="`toast-${index}`"
            :type="toast.type"
            :description="toast.description"
            :hideClose="toast.hideClose"
            :actions="toast.actions"
            :timeout="toast.timeout"
        />
        
    </ul>    
</template>
<script>
import ToastItem from './ToastItem'
export default {
    components: {
        ToastItem
    },
    data () {
        return {
            toasts: [
                
            ]
        }
    },
    created () {
        const types = ['info', 'success', 'danger', 'alert']
        for (let i = 0; i< 10; i++)
        this.toasts.push({
            type: types[i % 4], 
            description: '0 Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry\'s standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book.Lorem Ipsum is simply dummy text of the printing and typesetting industry.',
            hideClose: Math.random() > 0.5,
            timeout: Math.random() * 5000,
            actions: [{
                title: "OK",
                onClick: function() {alert('ok')}
            },
            {
                title: "Cancel",
                onClick: function() {alert('cancel')}
            }]
        })
    }


}
</script>
<style lang="scss">
    @import '../sass/toast.scss';
</style>