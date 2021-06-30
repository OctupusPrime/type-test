<template>
    <article class="type-test-container">
        <h1 class="type-test-title">|</h1>
        <div class="type-test-body">
            <div class="type-test-body-letter-row" :style="translateX">
                <span class="body-letter" v-for="(letter, index) in arrayOfText" :key="index" 
                                            :class="{'green': (index === rightLetter && !isRed), 'red': (index === rightLetter && isRed)}">
                    {{letter}}                 
                </span>
            </div>
        </div>
    </article>    
</template>

<script>
let rowLetters = null;
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
            isCaps: false,
            rightLetter: 0,
            isRed: false,
            offsetX: 0,

            timerVal: 60
        }
    },
    computed: {
        arrayOfText() {
            return this.testText.split('')
        },
        translateX() {
            return `transform: translateX(${-this.offsetX}px);`
        }
    },
    watch: {
        'rightLetter' () {
            this.offsetX += rowLetters[this.rightLetter-1].getBoundingClientRect().width/2 + rowLetters[this.rightLetter].getBoundingClientRect().width/2
        }
    },
    methods: {
        checkLetter(e) {
            switch(e.key) {
                case 'Backspace':
                    this.isRed = false 
                    break
                case 'CapsLock':
                    this.isCaps = !this.isCaps;
                    break
                case this.arrayOfText[this.rightLetter]:
                    if (this.rightLetter < 1)
                        this.timer(60)
                    
                    if (this.arrayOfText[this.rightLetter] === ' ')
                        console.log('end of word')

                    this.rightLetter++
                    this.isRed = false
                    break
                default:
                    this.isRed = true
                    break
            }
        },
        timer(end) {
            let i = end
            setInterval(function() {
                if (i < 0)
                    return clearInterval()
                
                console.log(i--);
            }.bind(this), 1000)
        }
    },
    mounted() {
        window.addEventListener('keydown', function ($event) {
            this.checkLetter($event)
        }.bind(this))

        rowLetters = document.querySelectorAll('.body-letter')
        this.offsetX = rowLetters[0].getBoundingClientRect().width/2
    }
}
</script>

<style scoped>
.type-test-container {
    margin: 0 auto;
    max-width: 750px;
    width: 95%;
}
.type-test-body {
    position: relative;
    padding-left: 50%;
    overflow: hidden;
}
.type-test-body-letter-row {
    display: flex;
    align-items: stretch;
}
.body-letter {
    display: inline-block;
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