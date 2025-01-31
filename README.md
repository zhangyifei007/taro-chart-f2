# remax-chart-f2
remax-chart-f2

*目前支持: 微信小程序*


F2图表具体使用方法请参考: https://github.com/antvis/f2


## 安装

```bash
$ npm i -S remax-chart-f2
```

## 用法

```javascript
import { F2Canvas } from 'remax-chart-f2'
```

## 示例

```javascript
import React, { Component } from 'react'
import { View } from 'remax/wechat'
import { F2Canvas } from 'remax-chart-f2'

// 绘制实例
const draw = [
  {chart: null, data: []}
]

export default class Index extends Component {
  componentDidMount() {
    let chartData = [
      { name: '超大盘能力', value: 6.5 },
      { name: '抗跌能力', value: 9.5 },
      { name: '稳定能力', value: 9 },
      { name: '绝对收益能力', value: 6 },
      { name: '选证择时能力', value: 6 },
      { name: '风险回报能力', value: 8 }
    ]
    // 模拟异步请求
    setTimeout(() => {
      draw[0].chart.source(chartData)
      draw[0].chart.repaint()
    }, 600)
  }

  drawRadar(num, canvas, width, height, F2){
    let data = draw[num].data
    let chart = new F2.Chart({
      el: canvas,
      width,
      height
    });
    chart.source(data, {
      value: {
        min: 0,
        max: 10
      }
    });
    chart.coord('polar');
    chart.axis('value', {
      grid: {
        lineDash: null
      },
      label: null,
      line: null
    });
    chart.axis('name', {
      grid: {
        lineDash: null
      }
    });
    chart.area()
      .position('name*value')
      .color('#FE5C5B')
      .style({
        fillOpacity: 0.2
      })
      .animate({
        appear: {
          animation: 'groupWaveIn'
        }
      });
    chart.line()
      .position('name*value')
      .color('#FE5C5B')
      .size(1)
      .animate({
        appear: {
          animation: 'groupWaveIn'
        }
      });
    chart.point().position('name*value').color('#FE5C5B').animate({
      appear: {
        delay: 300
      }
    });
    chart.guide().text({
      position: ['50%', '50%'],
      content: '73',
      style: {
        fontSize: 32,
        fontWeight: 'bold',
        fill: '#FE5C5B'
      }
    });
    chart.render();
    draw[num].chart = chart
  }

  render () {
    return (
      <View className='index'>
        <View style='width:100%;height:500px'>
          <F2Canvas onInit={this.drawRadar.bind(this, 0)}></F2Canvas>
        </View>
      </View>
    )
  }
}
```


