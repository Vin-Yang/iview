<template>
	<div :class="anchorLinkClasses">
        <a :class="linkTitleClasses" :href="href" :data-href="href" @click.prevent="goAnchor" :title="title">{{ title }}</a>
        <slot></slot>
    </div>
</template>
<script>
export default {
    name: 'AnchorLink',
    inject: ['anchorCom'],
    props: {
        href: String,
        title: String
    },
    data () {
        return {
            prefix: 'ivu-anchor-link'
        };
    },
    computed: {
        anchorLinkClasses () {
            return [
                this.prefix,
                this.anchorCom.currentLink === this.href ? `${this.prefix}-active` : ''
            ];
        },
        linkTitleClasses () {
            return [
                `${this.prefix}-title`
            ];
        }
    },
    methods: {
        goAnchor () {
            this.anchorCom.turnTo(this.href);
        }
    },
    mounted () {
        this.$nextTick(() => {
            this.anchorCom.init();
        });
    }
};
</script>
