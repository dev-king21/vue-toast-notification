<template>
    <li :class="`el-toast__item el-toast__item--${type}`" v-if="!removed">
        <div class="el-toast__icon">
            <i :class="`fa ${typeIcon}`"></i>
        </div>
        <div class="el-toast__close" v-if="!hideClose">
            <button @click="removed = true">
                <i class="fa fa-fw fa-times"></i>
            </button>
        </div>
        <div class="el-toast__description">
            {{descText}}
            <button v-if="isLong" @click="short = !short">{{viewMore}}</button>
        </div>
        <div class="el-toast__action">
            <button v-for="(act, index) in actions" :key="`action-button-${index}`" @click="act.onClick">{{act.title}}</button>
        </div>
        <div class="el-toast__progress" v-if="timeout && progress > 0">
            <div class="el-toast__bar" :style="`width: ${progress}%;`"></div>
        </div>
    </li>
</template>
<script>
export default {
    props: {
        type: {
            type: String,
            required: false,
            default: 'info'
        },
        description: {
            type: String,
            required: false,
            default: ''
        },
        timeout: {
            type: Number,
            required: false,
            default: 3000
        },
        onClose: {
            type: Function,
            required: false
        },
        hideClose: {
            type: Boolean,
            required: false,
            default: false
        },
        actions: {
            type: Array,
            required: false
        }
    },
    data () {
        return {
            short: true,
            progress: 100,
            removed: false
        }
    },
    computed: {
        typeIcon () {
            switch(this.type) {
                case 'danger': 
                    return 'fa fa-exclamation-triangle'
                case 'success': 
                    return 'fa fa-check-circle'
                case 'alert': 
                    return 'fa fa-exclamation-triangle'
                case 'info':
                default:
                    return 'fa fa-exclamation-circle'
            }
        },
        isLong () {
            return this.description && this.description.length > 80
        },
        descText () {
            if (this.isLong && this.short)
                return `${this.description.substring(0, 70)}...`
            return this.description
        },
        viewMore () {
            return this.short? 'View more' : 'View less'
        }
    },
    methods: {
        
    },
    mounted () {
        let interval = setInterval(() => {
            this.progress -= 10000  / this.timeout;
            if (this.progress <= 0) {
                this.progress = 0
                this.removed = true
                clearInterval(interval)
            }
        }, 100)
    }

}
</script>