<template>
  <div class="container">
    <ul class="example-list">
      <li class="example-item" @click="show">
          <span class="open">{{selectedText}}</span>
      </li>
    </ul>
    <transition name="picker-fade">
      <div class="picker" v-show="state===1" @touchmove.prevent @click="_cancel">
        <transition name="picker-move">
          <div class="picker-panel" v-show="state===1" @click.stop>
            <div class="picker-choose border-bottom-1px">
              <span class="cancel" @click="_cancel">Cancel</span>
              <span class="confirm" @click="_confirm">Confirm</span>
              <h1 class="picker-title">Title</h1>
            </div>
            <div class="picker-content">
              <div class="mask-top border-bottom-1px"></div>
              <div class="mask-bottom border-top-1px"></div>
              <div class="wheel-wrapper" ref="wheelWrapper">
                <div class="wheel" v-for="(data, index) in pickerData" :key="index">
                  <ul class="wheel-scroll">
                    <li
                      v-for="item in data" :key="item.value"
                      :class="{'wheel-disabled-item':item.disabled}"
                      class="wheel-item">{{item.text}}</li>
                  </ul>
                </div>
              </div>
            </div>
            <div class="picker-footer"></div>
          </div>
        </transition>
      </div>
    </transition>
  </div>
</template>

<script type="text/ecmascript-6">
  import BScroll from '@better-scroll/core'
  import Wheel from '@better-scroll/wheel'
  BScroll.use(Wheel)

  const STATE_HIDE = 0
  const STATE_SHOW = 1

  const COMPONENT_NAME = 'picker'
  const EVENT_SELECT = 'select'
  const EVENT_CANCEL = 'cancel'
  const EVENT_CHANGE = 'change'

  const DATA = [
    {
      text: '北京市',
      value: '110000',
      children: [
        {
          text: "北京市",
          value: '110100',
          children: [
            {
              value: '110101',
              text: '东城区',
            },
            {
              value: '110102',
              text: '西城区',
            },
            {
              value: '110105',
              text: '朝阳区',
            },
            {
              value: '110106',
              text: '丰台区',
            },
            {
              value: '110107',
              text: '石景山区',
            },
            {
              value: '110108',
              text: '海淀区',
            },
            {
              value: '110109',
              text: '门头沟区',
            },
            {
              value: '110111',
              text: '房山区',
            },
            {
              value: '110112',
              text: '通州区',
            },
            {
              value: '110113',
              text: '顺义区',
            },
            {
              value: '110114',
              text: '昌平区',
            },
            {
              value: '110115',
              text: '大兴区',
            },
            {
              value: '110116',
              text: '怀柔区',
            },
            {
              value: '110117',
              text: '平谷区',
            },
            {
              value: '110118',
              text: '密云区',
            },
            {
              value: '110119',
              text: '延庆区',
            },
          ],
        }
      ]
    },
    {
      text: '天津市',
      value: '120000',
      children: [
        {
          text: "天津市",
          value: '120000',
          children: [
            {
              value: '120101',
              text: '和平区',
            },
            {
              value: '120102',
              text: '河东区',
            },
            {
              value: '120103',
              text: '河西区',
            },
            {
              value: '120104',
              text: '南开区',
            },
            {
              value: '120105',
              text: '河北区',
            },
            {
              value: '120106',
              text: '红桥区',
            },
            {
              value: '120110',
              text: '东丽区',
            },
            {
              value: '120111',
              text: '西青区',
            },
            {
              value: '120112',
              text: '津南区',
            },
            {
              value: '120113',
              text: '北辰区',
            },
            {
              value: '120114',
              text: '武清区',
            },
            {
              value: '120115',
              text: '宝坻区',
            },
            {
              value: '120116',
              text: '滨海新区',
            },
            {
              value: '120117',
              text: '宁河区',
            },
            {
              value: '120118',
              text: '静海区',
            },
            {
              value: '120119',
              text: '蓟州区',
            },
          ],
        }
      ]
    },
    {
      text: '河北省',
      value: '130000',
      children: [
        {
          text: '石家庄市',
          value: '130100',
          children: [
            {
              value: '130102',
              text: '长安区',
            },
            {
              value: '130104',
              text: '桥西区',
            },
            {
              value: '130105',
              text: '新华区',
            },
            {
              value: '130107',
              text: '井陉矿区',
            },
            {
              value: '130108',
              text: '裕华区',
            },
            {
              value: '130109',
              text: '藁城区',
            },
            {
              value: '130110',
              text: '鹿泉区',
            },
            {
              value: '130111',
              text: '栾城区',
            },
            {
              value: '130121',
              text: '井陉县',
            },
            {
              value: '130123',
              text: '正定县',
            },
            {
              value: '130125',
              text: '行唐县',
            },
            {
              value: '130126',
              text: '灵寿县',
            },
            {
              value: '130127',
              text: '高邑县',
            },
            {
              value: '130128',
              text: '深泽县',
            },
            {
              value: '130129',
              text: '赞皇县',
            },
            {
              value: '130130',
              text: '无极县',
            },
            {
              value: '130131',
              text: '平山县',
            },
            {
              value: '130132',
              text: '元氏县',
            },
            {
              value: '130133',
              text: '赵县',
            },
            {
              value: '130181',
              text: '辛集市',
            },
            {
              value: '130183',
              text: '晋州市',
            },
            {
              value: '130184',
              text: '新乐市',
            },
          ],
        },
        {
          text: '唐山市',
          value: '130200',
          children: [
            {
              value: '130202',
              text: '路南区',
            },
            {
              value: '130203',
              text: '路北区',
            },
            {
              value: '130204',
              text: '古冶区',
            },
            {
              value: '130205',
              text: '开平区',
            },
            {
              value: '130207',
              text: '丰南区',
            },
            {
              value: '130208',
              text: '丰润区',
            },
            {
              value: '130209',
              text: '曹妃甸区',
            },
            {
              value: '130223',
              text: '滦县',
            },
            {
              value: '130224',
              text: '滦南县',
            },
            {
              value: '130225',
              text: '乐亭县',
            },
            {
              value: '130227',
              text: '迁西县',
            },
            {
              value: '130229',
              text: '玉田县',
            },
            {
              value: '130281',
              text: '遵化市',
            },
            {
              value: '130283',
              text: '迁安市',
            },
          ],
        },
        {
          value: '130300',
          text: '秦皇岛市',
          children: [
            {
              value: '130302',
              text: '海港区',
            },
            {
              value: '130303',
              text: '山海关区',
            },
            {
              value: '130304',
              text: '北戴河区',
            },
            {
              value: '130306',
              text: '抚宁区',
            },
            {
              value: '130321',
              text: '青龙满族自治县',
            },
            {
              value: '130322',
              text: '昌黎县',
            },
            {
              value: '130324',
              text: '卢龙县',
            },
          ],
        },
        {
          value: '130400',
          text: '邯郸市',
          children: [
            {
              value: '130402',
              text: '邯山区',
            },
            {
              value: '130403',
              text: '丛台区',
            },
            {
              value: '130404',
              text: '复兴区',
            },
            {
              value: '130406',
              text: '峰峰矿区',
            },
            {
              value: '130421',
              text: '邯郸县',
            },
            {
              value: '130423',
              text: '临漳县',
            },
            {
              value: '130424',
              text: '成安县',
            },
            {
              value: '130425',
              text: '大名县',
            },
            {
              value: '130426',
              text: '涉县',
            },
            {
              value: '130427',
              text: '磁县',
            },
            {
              value: '130428',
              text: '肥乡县',
            },
            {
              value: '130429',
              text: '永年县',
            },
            {
              value: '130430',
              text: '邱县',
            },
            {
              value: '130431',
              text: '鸡泽县',
            },
            {
              value: '130432',
              text: '广平县',
            },
            {
              value: '130433',
              text: '馆陶县',
            },
            {
              value: '130434',
              text: '魏县',
            },
            {
              value: '130435',
              text: '曲周县',
            },
            {
              value: '130481',
              text: '武安市',
            },
          ],
        },
      ]
    },
  ]

  export default {
    name: COMPONENT_NAME,
    data() {
      return {
        state: STATE_HIDE,
        selectedIndex: [0, 0, 0],
        selectedText: 'open',
        pickerData: []
      }
    },
    created () {
      // generate data
      // like [[{text: 'province1', value: '1'}, {text: 'province2', value: '2'}], [{text: 'city1', value: '11'}, {text: 'city2', value: '22'}]
      // pickerData has two array, the first is province collections, second is city collections
      this._loadPickerData(this.selectedIndex, undefined /* no prevSelectedIndex due to instantiating */)
    },
    methods: {
      _loadPickerData (newSelectedIndex, oldSelectedIndex) {
        // let provinces
        // let cities
        // // first instantiated
        // if (!oldSelectedIndex) {
        //   provinces = DATA.map(({ value, text }) => ({ value, text }))
        //   cities = DATA[newSelectedIndex[0]].children
        //   this.pickerData = [provinces, cities]
        // } else {
        //   // provinces'index changed, refresh cities data
        //   if (newSelectedIndex[0] !== oldSelectedIndex[0]) {
        //     cities = DATA[newSelectedIndex[0]].children
        //     this.pickerData.splice(1, 1, cities)
        //     // Since cities data changed
        //     // refresh better-scroll to recaculate scrollHeight
        //     this.$nextTick(() => {
        //       this.wheels[1].refresh()
        //     })
        //   }
        // }
        let columns = DATA

        if (!oldSelectedIndex) {
          let i = 0
          do {
            let columnData = columns.map(({ text, value }) => ({ text, value }))
            this.pickerData.push(columnData)
            i++
            columns = columns[newSelectedIndex[i]] && columns[newSelectedIndex[i]].children
          } while(columns)
        } else {
          console.log('newSelectedIndex', newSelectedIndex)
          console.log('oldSelectedIndex', oldSelectedIndex)

          let i = 0
          if (newSelectedIndex[0] !== oldSelectedIndex[0]) {
            let column = columns[newSelectedIndex[0]].children
            this.pickerData.splice(1, 1, column)

            this.$nextTick(() => {
              this.wheels[1].refresh()
            })
          }
        }
      },
      _confirm() {
        if (this._isMoving()) {
          return
        }
        this.hide()

        const currentSelectedIndex = this.selectedIndex = this.wheels.map(wheel => {
          return wheel.getSelectedIndex()
        })

        // store array for preventing multi-collecting array dependencies in Vue Source code
        const pickerData = this.pickerData
        const currentSelectedValue =
              this.selectedText =
                pickerData.map((data, index) => {
                  return data[currentSelectedIndex[index]].text
                }).join('-')
        this.$emit(EVENT_SELECT, currentSelectedIndex, currentSelectedValue)
      },
      _cancel() {
        this.hide()
        this.$emit(EVENT_CANCEL)
      },
      _isMoving() {
        return this.wheels.some((wheel) => {
          return wheel.pending
        })
      },
      show() {
        if (this.state === STATE_SHOW) {
          return
        }
        this.state = STATE_SHOW
        if (!this.wheels) {
          this.$nextTick(() => {
            this.wheels = []
            let wheelWrapper = this.$refs.wheelWrapper
            for (let i = 0; i < this.pickerData.length; i++) {
              this._createWheel(wheelWrapper, i)
            }
          })
        } else {
          for (let i = 0; i < this.pickerData.length; i++) {
            this.wheels[i].enable()
            this.wheels[i].wheelTo(this.selectedIndex[i])
          }
        }
      },
      hide() {
        this.state = STATE_HIDE

        for (let i = 0; i < this.pickerData.length; i++) {
          this.wheels[i].disable()
        }
      },
      refresh() {
        this.$nextTick(() => {
          this.wheels.forEach((wheel, index) => {
            wheel.refresh()
          })
        })
      },
      _createWheel(wheelWrapper, i) {
        const wheels = this.wheels
        if (!wheels[i]) {
          wheels[i] = new BScroll(wheelWrapper.children[i], {
            wheel: {
              selectedIndex: this.selectedIndex[i],
              wheelWrapperClass: 'wheel-scroll',
              wheelItemClass: 'wheel-item'
            },
            probeType: 3
          })
          // when any of wheels'scrolling ended , you should refresh data
          let prevSelectedIndex = this.selectedIndex
          wheels[i].on('scrollEnd', () => {
            console.log(111)
            const currentSelectedIndex = wheels.map(wheel => wheel.getSelectedIndex())
            this._loadPickerData(currentSelectedIndex, prevSelectedIndex)
            prevSelectedIndex = currentSelectedIndex
            this.$emit(EVENT_CHANGE, i, this.wheels[i].getSelectedIndex())
          })
        } else {
          this.wheels[i].refresh()
        }

        return this.wheels[i]
      }
    }
  }
</script>

<style scoped lang="stylus" rel="stylesheet/stylus">

  /* reset */
  ul
    list-style none
    padding 0

  .example-list
    display: flex
    justify-content: space-between
    flex-wrap: wrap
    margin: 2rem

    .example-item
      background-color white
      padding: 0.8rem
      border: 1px solid rgba(0, 0, 0, .1)
      box-shadow: 0 1px 2px 0 rgba(0,0,0,0.1)
      text-align: center
      margin-bottom: 1rem
      flex: 1
      &.placeholder
        visibility: hidden
        height: 0
        margin: 0
        padding: 0

  .picker
    position: fixed
    left: 0
    top: 0
    z-index: 100
    width: 100%
    height: 100%
    overflow: hidden
    text-align: center
    font-size: 14px
    background-color: rgba(37, 38, 45, .4)
    &.picker-fade-enter, &.picker-fade-leave-active
      opacity: 0
    &.picker-fade-enter-active, &.picker-fade-leave-active
      transition: all .3s ease-in-out

    .picker-panel
      position: absolute
      z-index: 600
      bottom: 0
      width: 100%
      height: 273px
      background: white
      &.picker-move-enter, &.picker-move-leave-active
        transform: translate3d(0, 273px, 0)
      &.picker-move-enter-active, &.picker-move-leave-active
        transition: all .3s ease-in-out
      .picker-choose
        position: relative
        height: 60px
        color: #999
        .picker-title
          margin: 0
          line-height: 60px
          font-weight: normal
          text-align: center
          font-size: 18px
          color: #333
        .confirm, .cancel
          position: absolute
          top: 6px
          padding: 16px
          font-size: 14px
        .confirm
          right: 0
          color: #007bff
          &:active
            color: #5aaaff
        .cancel
          left: 0
          &:active
            color: #c2c2c2
      .picker-content
        position: relative
        top: 20px
        .mask-top, .mask-bottom
          z-index: 10
          width: 100%
          height: 68px
          pointer-events: none
          transform: translateZ(0)
        .mask-top
          position: absolute
          top: 0
          background: linear-gradient(to top, rgba(255, 255, 255, 0.4), rgba(255, 255, 255, 0.8))
        .mask-bottom
          position: absolute
          bottom: 1px
          background: linear-gradient(to bottom, rgba(255, 255, 255, 0.4), rgba(255, 255, 255, 0.8))
      .wheel-wrapper
        display: flex
        padding: 0 16px
        .wheel
          -ms-flex: 1 1 0.000000001px
          -webkit-box-flex: 1
          -webkit-flex: 1
          flex: 1
          -webkit-flex-basis: 0.000000001px
          flex-basis: 0.000000001px
          width: 1%
          height: 173px
          overflow: hidden
          font-size: 18px
          .wheel-scroll
            padding: 0
            margin-top: 68px
            line-height: 36px
            list-style: none
            .wheel-item
              list-style: none
              height: 36px
              overflow: hidden
              white-space: nowrap
              color: #333
              &.wheel-disabled-item
                opacity: .2;
    .picker-footer
      height: 20px
</style>
