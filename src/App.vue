<template>
    <div id="app">
        <div class="videoBox">
            <div class="topBox" v-on:click="allRandomPosition">
                <div class="leftBox"></div>
                <div class="centerBox">
                    <div class="tip">当前期：</div>
                </div>
                <div class="rightBox">
                    <div class="soundButton"></div>
                    <div class="information">
                        <div>下期：</div>
                        <div>开奖：</div>
                    </div>
                </div>
            </div>
            <div class="countDown">00:00:00</div>
            <div class="middleBox">
                <ul id="init">
                    <li v-for="key in array" :key="key" :style="randomPosition()">{{key}}</li>
                </ul>
            </div>
            <div class="bottomBox">
                <button v-on:click="start"/>
                <ul class="result1">
                    <li v-for="key in result1" :key="key">{{key}}</li>
                </ul>
                <ul class="result2">
                    <li v-for="key in result2" :key="key">{{key}}</li>
                </ul>
            </div>
        </div>
    </div>

</template>

<script>
    export default {
        data() {
            return {
                array: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20],
                result: [],
                result1: [],
                result2: [],
                list: []
            }
        },

        methods: {
            randomPosition() {
                const x = 70 + Math.round(Math.random() * 178)
                return {
                    left: x + 'px',
                    top: 223 + 'px'
                }
            },
            allRandomPosition() {
                const ul = document.getElementById('init')
                const lis = ul.childNodes
                for (let i = 0; i < 100; i++) {
                    this.$data.list.push([this.positionX(), this.positionY()])
                }

                const id = setInterval(() => {
                    for (let i = 0; i < 20; i++) {
                        const index = Math.floor((Math.random() * 100))
                        lis[i].style.cssText = `left:${this.$data.list[index][0]}px;top:${this.$data.list[index][1]}px`
                    }
                }, 30)
                setInterval(() => {
                    window.clearInterval(id)
                    ul.childNodes.forEach(item => item.style.top = 230 + 'px')

                }, 3000)
            },
            positionX() {
                const x = 30 + Math.round(Math.random() * 260)
                return x
            },
            positionY() {
                const y = Math.round(Math.random() * 223)
                return y
            },
            reset() {
                this.$data.array = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20]
                this.$data.result = []
                this.$data.result1 = []
                this.$data.result2 = []
                this.randomPosition()
            },
            start() {
                this.allRandomPosition()
                setTimeout(this.run, 3000)
                setTimeout(this.reset, 8000)
            },
            run() {
                const arrayCopy = this.$data.array
                let i = 0, delNum, delArr
                for (i = 0; i < 8; i++) {
                    delNum = Math.floor(Math.random() * arrayCopy.length)
                    delArr = arrayCopy.splice(delNum, 1)
                    this.$data.result = this.$data.result.concat(delArr)
                }
                this.$data.result1 = this.$data.result.splice(0, 4)
                this.$data.result2 = this.$data.result
                console.log(this.$data.result1, this.$data.result2)
                return [this.$data.result1, this.$data.result2]
            },
        }
    }

</script>


<style lang="scss">

    @import "./assets/style/reset.scss";

    #app {
        width: 1125px;
        height: 750px;
        margin: 0 auto;

        > .videoBox {
            width: 100%;
            height: 100%;
            background: url("./assets/big_bg.png") 0 0 no-repeat;
            position: relative;

            > .topBox {
                height: 120px;
                display: flex;

                > .leftBox {
                    width: 25%;
                }

                > .centerBox {
                    width: 50%;
                    position: relative;

                    > .tip {

                        position: absolute;
                        color: #fff;
                        font-size: 20px;
                        bottom: 0;
                        left: 50%;
                        transform: translateX(-50%);
                    }
                }

                > .rightBox {
                    width: 25%;
                    position: relative;

                    > .soundButton {
                        width: 50px;
                        height: 50px;
                        position: absolute;
                        top: 15%;
                        left: 10%;
                        background: url("./assets/sound.png");
                    }

                    > .information {
                        position: absolute;
                        width: 150px;
                        height: 50px;
                        top: 15%;
                        left: 40%;
                        color: #fff;
                        font-size: 16px;
                    }
                }
            }

            > .countDown {
                position: absolute;
                width: 215px;
                height: 55px;
                top: 139px;
                left: 455px;
                font-family: 'DS-Digital';
                color: #fff000;
                font-size: 52px;
                text-align: center;

            }

            > .middleBox {
                position: absolute;
                width: 385px;
                height: 300px;
                left: 370px;
                top: 223px;
                border-radius: 30% 30% 37% 35%;

                > ul {
                    position: relative;


                    > li {
                        position: absolute;
                        text-align: center;
                        font-size: 30px;
                        width: 62px;
                        height: 62px;
                        background: url("./assets/light_skyblue.png") no-repeat;
                        top: 223px;
                        left: 150px;
                        font-family: Arial Bold;
                        font-weight: 600;
                    }
                }

            }

            > .bottomBox {
                display: flex;
                justify-content: space-between;
                position: absolute;
                height: 80px;
                width: 630px;
                top: 598px;
                left: 244px;

                > button {
                    width: 80px;
                    height: 80px;
                    position: absolute;
                    top: -11px;
                    left: 277px;
                    border-radius: 50%;
                    background: transparent;
                    border: transparent;
                }


                > .result1 {
                    height: 80px;
                    width: 250px;
                    display: flex;
                    justify-content: space-between;
                    align-items: center;

                    > li {
                        width: 62px;
                        height: 62px;
                        background: url("./assets/light_skyblue.png") no-repeat;
                        text-align: center;
                        font-size: 30px;
                        font-family: Arial Bold;
                        font-weight: 600;
                        padding-top: 10px;

                    }
                }

                > .result2 {
                    height: 80px;
                    width: 250px;
                    display: flex;
                    justify-content: space-between;
                    align-items: center;

                    > li {
                        width: 62px;
                        height: 62px;
                        background: url("./assets/light_skyblue.png") no-repeat;
                        text-align: center;
                        font-size: 30px;
                        font-family: Arial Bold;
                        font-weight: 600;
                        padding-top: 10px;

                    }
                }
            }
        }
    }


</style>
