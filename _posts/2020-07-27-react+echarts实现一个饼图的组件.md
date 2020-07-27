---
title: react+echarts实现一个饼图的组件
tags: Lin
---
**npm安装echarts-for-react**

	npm install --save echarts-for-react
	npm install echarts --save
	
**引入模块和组件**

	import React from 'react';
	
	import echarts from 'echarts/lib/echarts'
	import 'echarts/lib/chart/pie';  //折线图是line,饼图改为pie,柱形图改为bar
	import 'echarts/lib/component/tooltip';
	import 'echarts/lib/component/title';
	import 'echarts/lib/component/legend';
	
**配置option参数**

写在一个单独的文件config.js文件，然后module.exports导出

	let colors = ['#E60012', '#EB6100', '#F39800', '#FFF100', '#8FC31F', '#22AC38', '#009944', '#009E96', '#0068B7', '#601986']
	module.exports = {
	    color: colors,
	    title: {
	        text: '设备类型统计',
	        left: 'left',
	        top: '2%',
	        textStyle: {
	            color: '#fff'
	        }
	    },
	    tooltip: {
	        trigger: 'item',
	        formatter: '{a} <br/>{b} : {c} ({d}%)'
	    },
	
	    series: [
	
	        {
	            name: '类型统计',
	            type: 'pie',//饼图
	            radius: [30, 110],
	            roseType: 'area',
	            data: [],//数据后面再导入
	            //设置显示标签的样式
	            label: {
	                position: 'outside',
	                color: '#0DD5ED',
	                // formatter: '{b} \n\n {d}%',
	                formatter: function (data) {
	                    return data.name + ' \n\n ' + data.percent.toFixed(1) + '%'
	                },
	                padding: [0, -30, 0, -30],
	            },
	            //设置线条样式
	            labelLine: {
	                length: 10,
	                length2: 30,
	                lineStyle: {
	                    width: 1
	                }
	            },
	        }
	    ]
	};
	
**组件初始化**

我使用的是class组件

	import React from 'react';
	
	import echarts from 'echarts/lib/echarts'
	import 'echarts/lib/chart/pie';  //折线图是line,饼图改为pie,柱形图改为bar
	import 'echarts/lib/component/tooltip';
	import 'echarts/lib/component/title';
	import 'echarts/lib/component/legend';
	
	import config from './config.js'
	
	class PieDiv extends React.Component {
	    /**
	     * 初始化id id是随机生成的一串唯一的字符串
	     */
	    constructor(props) {
	        super(props)
	        let id = ('_' + Math.random()).replace('.', '_');
	        this.state = {
	            pieId: 'pie' + id
	        }
	    }
	    /**
	     * 生成图表，主要做了一个判断，因为如果不去判断dom有没有生成，
	     * 在后面如果定期去更新图表，每次生成一个dom节点会导致浏览器
	     * 占用的cpu和内存非常高，踩过坑。
	     * 这里的config就是引入的配置文件中的config,文件头部会有说明
	     */
	    initPie(id) {
	        let myChart = echarts.getInstanceByDom(document.getElementById(id));
	        if (myChart === undefined) {
	            myChart = echarts.init(document.getElementById(id));
	        }
	        myChart.setOption(config)
	    }
		//在其他地方引用的时候，把值传入list中，就可以使用改组件，
		//因为接口中查询到的不一定会直接渲染页面，所有采用componentWillReceiveProps生命
		//周期函数，在值发生变化的时候，重新传入值。
	    componentWillReceiveProps=(nextProps)=> {
	        
	        const {list:oldlist} = this.props
	        const {list:newlist} = nextProps
	        if(oldlist!=newlist){
	            config.series[0].data = newlist
	            this.initPie(this.state.pieId);
	        }
	    }
	    //使用组件的时候还需要传入一个height，因为echarts图表显示必须要有高度，没有高度无法显示图表
	    render() {
	        const {height} = this.props
	        return (
	            <div id={this.state.pieId} style={{ height }}></div>
	        )
	    }
	}
	
	export default PieDiv
**最后**

在其他地方引入，就可以使用这个饼图了

	import PieDiv from '***'
	<PieDiv height={400} list={this.state.DataArr}/>
	
传入的list数据格式如下

	data= [
	          { 
	            name: 'XXX',
	            value: 1 ,
	           },
	           { 
	             name: 'XXX',
	            value: 2 ,
	            },
	     ]
