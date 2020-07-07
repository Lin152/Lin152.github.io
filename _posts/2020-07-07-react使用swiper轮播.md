---
title: react+swiper
tags: Lin
---

首先引入，我这里使用是5.3.0

	npm i swiper@5.3.0 --save
	
然后在组件头部引入

	import Swiper from 'swiper';
	import 'swiper/css/swiper.css';
	
这里我使用的是class组件
初始化轮播组件

	componentDidMount() {
	        this.instanceSwiper()
	}
	   
	instanceSwiper() {
        this.swiperObj = new Swiper('.swiper-container', {
            slidesPerView: 1,
            loop: false,
            autoplay: {// 自动滑动
                delay: 3000, //3秒切换一次
                // stopOnLastSlide: false,
                disableOnInteraction: false,//
            },
            observer: true,//修改swiper自己或子元素时，自动初始化swiper    重要
            observeParents: true,//修改swiper的父元素时，自动初始化swiper  重要

        })

    }
 
数据改变的时候，重新渲染
 
	  componentDidUpdate() {
	        this.swiperObj.update();
	        this.swiperObj.slideTo(0, 1000, false);
	  }
	  
数据改变的时候可以会卡死，使用这个生命周期解决（list是传入的数据）。原理：当数据发生改变，先销毁swiper，再重新初始化。

	componentWillReceiveProps = (nextProps) => {
	        const { list: oldList } = this.props
	        const { list: newList } = nextProps
	        if (oldList != newList) {
	            this.swiperObj.destroy();
	            this.swiperObj = null;
	            this.instanceSwiper()
	        }
	    }



结束时销毁

	  componentWillUnmount() {
	        if (this.swiperObj.destroy) { // 销毁swiper
	            this.swiperObj.destroy();
	            this.swiperObj = null;
	       }
	  }

render()中使用固定的class样式，在react中class换成className,**swiper-container, swiper-no-swiping**,**swiper-wrapper**,**swiper-slide**这几个className属性为固定写法，不能修改，但是可以添加样式con，swiperFather为组件外层样式。con样式添加的原因是必须设置一个height，否则无法显示轮播效果


	render() {
	        const { list} = this.props
			return (
            <div className={styles.swiperFather}>
                {/* /swiper-no-swiping关闭鼠标滑动  ${styles.con}设置轮播组件的宽高*/}
                <div className={`swiper-container swiper-no-swiping ${styles.con}`} style={{ overflow: 'hidden' }}>
                    <div className={`swiper-wrapper ${styles.con}`}>
                        {
                            list && list.length > 0 && list.map((item, index) => {
                                    return (
                                        <div className="swiper-slide" key={`swiper${index}`}>
                                       			...more//添加自己的业务代码
                                       </div>
									)
									
							})
					</div>
				</div>
			</div>
		)
		}
		css样式
		.swiperFather {
		    width: 700px;
		    height: 570px;
		    margin-left: auto;
		    margin-right: auto;
		    position: relative;
		}
		.con {
	    	height: 570px;
		}


**这个只是我个人的解决办法，应该还有其他办法**
								                                         

