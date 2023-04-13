<template>
  <div class="box">
    <el-date-picker
      v-model="value2"
      type="daterange"
      align="right"
      unlink-panels
      range-separator="至"
      start-placeholder="开始日期"
      end-placeholder="结束日期"
      :picker-options="pickerOptions"
      @change="handleDateChange">
    </el-date-picker>
    <div class="container" :style="{width:`${ChartWidth}%`}">
      <GanttChart
        :key="key"
        :gantt-data="GanttData"
        :gantt-current-time="GanttCurrentTime"
        :first-line-stick="firstLineStick"
        :time-section="timeSection"
        :chart-max-height="ChartHeight"
        :float-view-render-fn="floatRender"
        @rightClick.native="handleRightClick"
        :header-data="headerData"
      >
        <template #side-box="{item}">
          <SideComponent :side-info="item" />
        </template>
<!--        <template #container-box="{item}">-->
<!--          <ContentComponent :content-info="item" />-->
<!--        </template>-->
      </GanttChart>
    </div>
<!--    <div class="operate__area">-->
<!--      <div id="buffer__area" class="drag-wrapper">-->
<!--        <span>可拖拽区域:</span>-->
<!--      </div>-->
<!--      <div class="operate">-->
<!--        <div>首行是否粘性:<el-switch v-model="firstLineStick" active-color="#13ce66" inactive-color="#ff4949" /></div>-->
<!--        <div>调节甘特图宽度:<el-slider v-model="ChartWidth" /></div>-->
<!--        <div>调节甘特图内容高度:<el-slider v-model="ChartHeight" :min="0" :max="600" /></div>-->
<!--      </div>-->
<!--    </div>-->
  </div>
</template>
<script>
import dayjs from 'dayjs'
import Drag from '../packages/vue-gantt-chart/src/unit/drag'
import SideComponent from './components/SideComponent'
import ContentComponent from './components/ContentComponent'
import { mockData } from './lib/mock'
export default {
  components: { ContentComponent, SideComponent },
  data () {
    return {
      key: -1,
      pickerOptions: {
        shortcuts: [{
          text: '最近一周',
          onClick (picker) {
            const end = new Date()
            const start = new Date()
            start.setTime(start.getTime() - 3600 * 1000 * 24 * 7)
            picker.$emit('pick', [start, end])
          }
        }, {
          text: '最近一个月',
          onClick (picker) {
            const end = new Date()
            const start = new Date()
            start.setTime(start.getTime() - 3600 * 1000 * 24 * 30)
            picker.$emit('pick', [start, end])
          }
        }, {
          text: '最近三个月',
          onClick (picker) {
            const end = new Date()
            const start = new Date()
            start.setTime(start.getTime() - 3600 * 1000 * 24 * 90)
            picker.$emit('pick', [start, end])
          }
        }]
      },
      value2: '',
      timeSection: [dayjs().format('YYYY/MM/DD'), dayjs().add(6, 'day').format('YYYY/MM/DD')],
      // GanttData: mockData(50),
      GanttData: [
        {
          id: 0,
          currentAirport: '张浩哲1',
          number: '',
          model: '',
          childArray: [
            {
              id: 0,
              startAirport: '天津机场',
              endAirport: '兰伯特-圣路易国际机场',
              workType: '',
              start: '2023/04/11 00:00',
              end: '2023/04/11 23:59'
            },
            {
              id: 1,
              startAirport: '达拉斯/沃思堡国际机场',
              endAirport: '塔尔萨国际机场',
              workType: '',
              start: '2023/04/12 00:00',
              end: '2023/04/12 23:59'
            },
            {
              id: 2,
              startAirport: '兰伯特-圣路易国际机场',
              endAirport: '塔尔萨国际机场',
              workType: '气象/资源保护',
              start: '2023/04/13 00:00',
              end: '2023/04/13 23:59'
            },
            {
              id: 3,
              startAirport: '天津机场3',
              endAirport: '兰伯特-圣路易国际机场3',
              workType: '夜视镜培训3',
              start: '2023/04/14 00:00',
              end: '2023/04/14 23:59'
            },
            {
              id: 4,
              startAirport: '达拉斯/沃思堡国际机场4',
              endAirport: '塔尔萨国际机场4',
              workType: '农林牧副渔生产4',
              start: '2023/04/15 00:00',
              end: '2023/04/15 23:59'
            },
            {
              id: 5,
              startAirport: '兰伯特-圣路易国际机场5',
              endAirport: '塔尔萨国际机场5',
              workType: '气象/资源保护5',
              start: '2023/04/16 00:00',
              end: '2023/04/16 23:59'
            },
            {
              id: 6,
              startAirport: '兰伯特-圣路易国际机场6',
              endAirport: '塔尔萨国际机场6',
              workType: '气象/资源保护6',
              start: '2023/04/17 00:00',
              end: '2023/04/17 23:59'
            }
          ]
        },
        {
          id: 1,
          currentAirport: '张浩哲2',
          number: '',
          model: '',
          childArray: [
            {
              id: 0,
              startAirport: '休士頓喬治布希洲際機場',
              endAirport: '天津机场',
              workType: '私人飞行',
              start: '2023/04/13 02:37',
              end: '2023/04/13 14:26'
            },
            {
              id: 1,
              startAirport: '休士頓喬治布希洲際機場',
              endAirport: '休士頓喬治布希洲際機場',
              workType: '医疗救援',
              start: '2023/04/12 12:37',
              end: '2023/04/12 19:04'
            },
            {
              id: 2,
              startAirport: '兰伯特-圣路易国际机场',
              endAirport: '天津机场',
              workType: 'VIP运输',
              start: '2023/04/12 11:37',
              end: '2023/04/12 20:19'
            }
          ]
        }
      ],
      GanttCurrentTime: new Date().getTime(),
      floatRender: (info) => `<div>${info.startAirport}</div><div>${info.workType}</div><div>${info.endAirport}</div>`,
      // 定时器
      marker: null,
      // 测试
      firstLineStick: true,
      ChartWidth: 100,
      ChartHeight: 600,
      headerData: ['人员']
    }
  },
  mounted () {
    console.log(this.value2)
    console.log(dayjs())
    console.log(this.timeSection)
    this.marker = setInterval(() => {
      this.GanttCurrentTime += 100000
    }, 1000)
    new Drag(document, true)
    const $testEle = document.querySelector('#buffer__area')
    const observerOptions = {
      childList: true,	// 观察目标子节点变换
      attributes: false,	// 观察属性变动
      subtree: true		// 观察后代节点
    }
    const nodeHash = {}
    const observer = new MutationObserver(function (mutationList) {
      mutationList.forEach(mutation => {
        if (mutation.addedNodes.length) { // 添加节点
          const obj = mutation.addedNodes[0]
          nodeHash[obj.id] = obj.style.left
          obj.style.position = 'relative'
          obj.style.left = '5px'
        }
        if (mutation.removedNodes.length) { // 移除节点
          const obj = mutation.removedNodes[0]
          obj.style.left = nodeHash[obj.id]
          obj.style.position = 'absolute'
        }
      })
    })
    observer.observe($testEle, observerOptions)
  },
  beforeDestroy () {
    clearInterval(this.marker)
  },
  methods: {
    handleDateChange (newDate) {
      // 在日期选择变化时调用的函数
      console.log('选中的日期：', newDate)
      // 执行其他操作
      console.log(this.newDate)
      console.log(dayjs())
      console.log(this.timeSection)
      this.timeSection = [dayjs(newDate[0]).format('YYYY/MM/DD'), dayjs(newDate[1]).format('YYYY/MM/DD')]
      this.key = Math.random()
      console.log(newDate)
      console.log(dayjs())
      console.log(this.timeSection)
    },
    handleRightClick (event) {
      console.log('event', event)
      console.log('timeSection', this.timeSection)
      console.log('GanttCurrentTime', this.GanttCurrentTime)
      console.log('floatRender', this.floatRender)
      console.log('marker', this.marker)
      console.log('GanttData', this.GanttData)
      const info = event.detail
      this.$notify.info({
        title: '消息',
        dangerouslyUseHTMLString: true,
        message: `
                <div>
                <strong>起飞机场</strong>:  ${info.startAirport}
                </div>
                <div>
                <strong>任务类型</strong>:  ${info.workType}</div>
                <div>
                <strong>降落机场</strong>:  ${info.endAirport}
                </div>`
      })
    }
  }
}
</script>

<style lang="scss" scoped>
.operate__area{
  width: 90vw;
  position: absolute;
  left: 50%;
  bottom: 1em;
  transform: translate(-50%,0);
  border: 1px solid #EBEEF5;
  border-radius: 5px;
  box-shadow: 0 2px 12px 0 rgba(0,0,0,.1);
  display: grid;
  grid-template-columns: 1fr 1fr;
  .operate > div{
    margin: 1em;
  }
}
#buffer__area{
  display: flex;
  margin: 5px;
  flex-direction: column;
  border: 3px dashed salmon;
}
</style>
