<template>
    <article class="type-test-container">
        <h1 class="type-test-title">Type test</h1>
        <div class="type-test-body">
            <span class="body-letter" v-for="(letter, index) in arrayOfText" :key="index" 
                                        :data-index="index"
                                        :class="{'green': (index === rightLetter && !isRed), 'red': (index === rightLetter && isRed)}">
                {{letter}}                 
            </span>
        </div>
    </article>    
</template>

<script>
export default {
    name: 'TypeTest',
    props: {
        testText: {
            type: String,
            required: true
        }
    },
    data: () => {
        return {
            rightLetter: 0,
            isRed: false
        }
    },
    computed: {
        arrayOfText() {
            return this.testText.split('')
        }
    },
    methods: {
        checkLetter(e) {
            if (e.keyCode === 8)
                return this.isRed = false

            if (e.key === this.arrayOfText[this.rightLetter]) {
                if (this.rightLetter++ === this.arrayOfText.length -1) {
                    return this.$emit('finished')
                }
                return this.isRed = false
            }

            this.isRed = true
        }
    },
    mounted() {
        window.addEventListener('keydown', function ($event) {
            this.checkLetter($event)
        }.bind(this))
    }
}
</script>

<style scoped>
.type-test-body {
    display: flex;
    justify-content: center;
    align-items: stretch;
    padding-bottom: 20px;
}
.body-letter {
    display: inline-block;
    min-width: 5px;
    margin: 0 0.025em;
    padding: 0.2em;
    border-radius: 2px;
    font-size: 20px;
}
.red {
    background: #e63946;
    color: #fff;
}
.green {
    background: #80b918;
    color: #fff;
}
</style>