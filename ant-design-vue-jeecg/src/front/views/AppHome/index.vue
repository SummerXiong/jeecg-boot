<template>
    <div class="app-home">
        <BaseBanner/>
        <div class="margin">
            <div class="home-product">
                <BaseBlock :baseBlockTitle="titleArr[0]" class="margin">
                    <div class="home-product-box">
                        <HomeTopCard class="home-product-item" v-for="(item, index) in productArr" :productObj="item" :class="'productActive' + index" :key="index"/>
                    </div>
                </BaseBlock>
            </div>
            <div class="home-solution">
                <BaseBlock :baseBlockTitle="titleArr[1]" class="margin">
                    <div class="swiper-container solution-swiper-container">
                        <div class="swiper-wrapper">
                            <div class="swiper-slide" v-for="item, index in solutionArr" :key="index">
                                <div class="home-solution-box">
                                    <div class="home-solution-item"
                                         v-for="item2, index2 in item"
                                         :key="index2"
                                         :class="('home-solution-item' + index2)"
                                         @mouseenter="solutionEnter(index, index2)"
                                         @mouseleave="solutionLeave()">
                                        <img :src="solutionIndex == '' + index + index2 ? item2.iconSrc2 : item2.iconSrc1"/>
                                        <div class="solution-item-right" :class="solutionIndex == '' + index + index2 ? 'solution-item-right-big' : ''">
                                            <h3>{{ item2.title }}</h3>
                                            <p>{{ item2.content }}</p>
                                            <span @click="goPage(item2.name)">查看详情</span>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                        <div class="swiper-button-prev"></div>
                        <div class="swiper-button-next"></div>
                    </div>
                </BaseBlock>
            </div>
            <div class="home-cases">
                <BaseBlock :baseBlockTitle="titleArr[2]">
                    <div class="home-cases-box">
                        <div v-for="(item, index) in caseArr" :key="index" :class="[index < 3 ? 'cases-margin-b' : '', 'home-cases-item']">
                            <div class="cases-item-industry">{{ item.industry }}</div>
                            <div class="case-item-main">
                                <h3>{{ item.title }}</h3>
                                <p>{{ item.content }}</p>
                            </div>
                            <span class="cases-item-more">了解详情 <i></i></span>
                            <img :src="item.imgSrc" />
                            <span class="cases-item-line"></span>
                        </div>
                        <div class="home-cases-item home-cases-more">
                            <div class="cases-item-industry">了解更多</div>
                            <div class="case-item-main">
                                <h3>点击这里了解更多行业案例</h3>
                                <p>点击这里了解更多行业案例，点击这里了解更多行业案点击这里了解更多行业案例点击这里了解更多行业案例，点击这里了解更多行业案例。</p>
                            </div>
                            <div class="case-img">
                                <img src="@assets/home/案例图.png" />
                                <img src="@assets/home/案例图.png" />
                                <img src="@assets/home/案例图.png" />
                            </div>
                            <span class="cases-item-line"></span>
                        </div>
                    </div>
                </BaseBlock>
            </div>
            <div class="home-partner">
                <BaseBlock :baseBlockTitle="titleArr[3]">
                    <div class="swiper-container partner-swiper-container">
                        <div class="swiper-wrapper">
                            <div class="swiper-slide" v-for="item, index in partnerArr" :key="index">
                                <div class="home-partner-box">
                                    <h3>{{ item.title }}</h3>
                                    <p>{{ item.content }}</p>
                                    <div class="partner-img">
                                        <div class="partner-img-item" v-for="item2, index2 in item.img" :key="index2">
                                            <img :src="item2.imgSrc" :alt="item2.name">
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                        <div class="swiper-pagination"></div>
                    </div>
                </BaseBlock>
            </div>
        </div>
    </div>
</template>

<script>
    import BaseBlock from '../../components/BaseBlock'
    import HomeTopCard from './components/HomeTopCard'
    import BaseBanner from '../../components/BaseBanner'
    import Swiper from 'swiper'

    export default {
        name: 'AppHome',
        components: { BaseBanner, HomeTopCard, BaseBlock },
        mounted() {
            //方案轮播图
            var solutionSwiper = new Swiper('.solution-swiper-container', {
                speed: 1000,
                navigation: {
                    nextEl: '.swiper-button-next',
                    prevEl: '.swiper-button-prev'
                }
            })
            //客户轮播图
            let partnerSwiper = new Swiper('.partner-swiper-container',{
                speed: 1000,
                pagination: {
                    el: '.swiper-pagination',
                    bulletClass : 'my-bullet',
                    bulletActiveClass: 'my-bullet-active-b',
                },
            })
        },
        data() {
            return {
                solutionIndex: '',
                //标题
                titleArr: [
                    { title: '产品介绍', titleEN: 'PRODUCT DESCRIPTION' },
                    { title: '解决方案', titleEN: 'INDUSTRY SOLUTIONS' },
                    { title: '行业案例', titleEN: 'INDUSTRY CASE' },
                    { title: '合作客户', titleEN: 'OUR CUSTOMERS' }
                ],
                //产品
                productArr: [
                    {
                        imgSrc: require('../../../assets/home/数据采集icon.png'),
                        title: '数据采集',
                        list: [
                            { name: '数据填报平台', path: ''},
                            { name: '数据补录平台', path: ''},
                            { name: '智慧采集平台', path: ''}
                        ]
                    },
                    {
                        imgSrc: require('../../../assets/home/数据处理icon.png'),
                        title: '数据处理',
                        list: [
                            { name: '一站式数据处理平台', path: ''},
                            { name: 'ETS调度管理平台', path: ''}
                        ]
                    },
                    {
                        imgSrc: require('../../../assets/home/数据治理icon.png'),
                        title: '数据治理',
                        list: [
                            { name: '智能数据治理平台', path: ''},
                            { name: '元数据管理平台', path: ''},
                            { name: '数据质量管理平台', path: ''},
                            { name: '主数据管理平台', path: ''},
                            { name: '数据共享交换平台', path: ''}
                        ]
                    },
                    {
                        imgSrc: require('../../../assets/home/数据分析icon.png'),
                        title: '数据分析',
                        list: [
                            { name: '一站式数据分析平台--帆软BI', path: ''},
                            { name: '数据分析展示平台--永洪BI', path: ''},
                            { name: '自助式数据分析平台--豌豆BI', path: ''},
                            { name: '数据可视化平台--HL智屏', path: ''},
                            { name: '数据挖掘平台--HLDM', path: ''}
                        ]
                    },
                    {
                        imgSrc: require('../../../assets/home/运营监控icon.png'),
                        title: '运营监控',
                        list: [
                            { name: '系统管理', path: ''},
                            { name: '系统监控', path: ''},
                            { name: '数据监控', path: ''},
                            { name: '数据价值', path: ''},
                            { name: '服务监控', path: ''}
                        ]
                    }
                ],
                //方案
                solutionArr: [
                    [
                        {
                            iconSrc1: require('@/assets/home/物联网未选中icon.png'),
                            iconSrc2: require('@/assets/home/物联网选中icon.png'),
                            title: '智慧金融解决方案',
                            content: '针对各类金融业务形态，海联产品将协助完成数据的搭建及监控，提高金融风险管控，用数据驱动资产积累。',
                            name: ''
                        },
                        {
                            iconSrc1: require('@/assets/home/物联网未选中icon.png'),
                            iconSrc2: require('@/assets/home/物联网选中icon.png'),
                            title: '智慧金融解决方案',
                            content: '针对各类金融业务形态，海联产品将协助完成数据的搭建及监控，提高金融风险管控，用数据驱动资产积累。',
                            name: ''
                        },
                        {
                            iconSrc1: require('@/assets/home/物联网未选中icon.png'),
                            iconSrc2: require('@/assets/home/物联网选中icon.png'),
                            title: '智慧金融解决方案',
                            content: '针对各类金融业务形态，海联产品将协助完成数据的搭建及监控，提高金融风险管控，用数据驱动资产积累。',
                            name: ''
                        },
                        {
                            iconSrc1: require('@/assets/home/物联网未选中icon.png'),
                            iconSrc2: require('@/assets/home/物联网选中icon.png'),
                            title: '智慧金融解决方案',
                            content: '针对各类金融业务形态，海联产品将协助完成数据的搭建及监控，提高金融风险管控，用数据驱动资产积累。',
                            name: ''
                        }
                    ],
                    [
                        {
                            iconSrc1: require('@/assets/home/物联网未选中icon.png'),
                            iconSrc2: require('@/assets/home/物联网选中icon.png'),
                            title: '智慧金融解决方案',
                            content: '针对各类金融业务形态，海联产品将协助完成数据的搭建及监控，提高金融风险管控，用数据驱动资产积累。',
                            name: ''
                        },
                        {
                            iconSrc1: require('@/assets/home/物联网未选中icon.png'),
                            iconSrc2: require('@/assets/home/物联网选中icon.png'),
                            title: '智慧金融解决方案',
                            content: '针对各类金融业务形态，海联产品将协助完成数据的搭建及监控，提高金融风险管控，用数据驱动资产积累。',
                            name: ''
                        },
                        {
                            iconSrc1: require('@/assets/home/物联网未选中icon.png'),
                            iconSrc2: require('@/assets/home/物联网选中icon.png'),
                            title: '智慧金融解决方案',
                            content: '针对各类金融业务形态，海联产品将协助完成数据的搭建及监控，提高金融风险管控，用数据驱动资产积累。',
                            name: ''
                        },
                        {
                            iconSrc1: require('@/assets/home/物联网未选中icon.png'),
                            iconSrc2: require('@/assets/home/物联网选中icon.png'),
                            title: '智慧金融解决方案',
                            content: '针对各类金融业务形态，海联产品将协助完成数据的搭建及监控，提高金融风险管控，用数据驱动资产积累。',
                            name: ''
                        }
                    ]
                ],
                //案例
                caseArr: [
                    {
                        name: '',
                        industry: '制造业',
                        title: '海尔供应商绩效评价系统',
                        content: '根据供应商分类和绩效确定差异化的产品及合作策略，从T（技术）Q（质量）R（响应）D（配送）C（成本）五个维度对供应商进行全方位的绩效管理，进一步提升企业对供应商精细化管控能力，提升效率与价值。',
                        imgSrc: require('@assets/home/案例图.png'),
                    },
                    {
                        name: '',
                        industry: '航空行业',
                        title: '青岛航空数据仓库项目',
                        content: '青岛航空内部各系统间相对较为独立，数据分散，产生信息孤岛，各部门获取的信息比较片面的，因此需要借助大数据技术手段，将机构各系统数据集中存储，统一管理。实现跨系统数据共享，解决信息孤岛，提升数据质量，为各层级用户提供统一的数据服务。',
                        imgSrc: require('@assets/home/案例图.png'),
                    },
                    {
                        name: '',
                        industry: '呼叫中心行业',
                        title: '日日顺乐信LeDC数据中心项目',
                        content: '乐信HIC大数据平台2013年建设，随着业务发展，原有平台处理效率及可靠性不能满足业务需求，在此基础上，借助海联产品及技术服务重建大数据平台，批量数据处理就挖掘的时效达到分钟级别，实时数据处理达到秒级响应，大大提升了业务处理的能力。',
                        imgSrc: require('@assets/home/案例图.png'),
                    },
                    {
                        name: '',
                        industry: '金融行业',
                        title: '青岛清算中心地方金融监管预警平台',
                        content: '青岛场外市场清算中心作为全国首家服务于场外市场的独立第三方清算机构，作为全国最影响力且接入现货交易场所最多的清算场所，建设一具备高效、全面、直观的风险监控平台以实时展示各交易市场运营状态、参数变动、异常操作等情况正是对监管机构和投资主体负责的体现。',
                        imgSrc: require('@assets/home/案例图.png'),
                    },
                    {
                        name: '',
                        industry: '征信行业',
                        title: '联信征信报告系统项目',
                        content: '随着经济市场化程度的不断加深发展，加快企业和个人征信体系的建设已成为社会共识。在此背景下，联信集团借助海联科技的技术手段，依法采集、客户记录其信用信息，对外提供信用信息服务，为联信搭建了一个信用信息共享系统，以便能够快速识别低信用客户，规避借贷欺诈风险。',
                        imgSrc: require('@assets/home/案例图.png'),
                    }
                ],
                //客户
                partnerArr: [
                    {
                        title: '金融行业',
                        content: '这里是金融行业介绍，这里是金融行业介绍，这里是金融行业相关介绍，这里是行业相关介绍，这里是行业相关介绍，这里是行业相关介绍。',
                        img: [
                            { name: '海尔', imgSrc: require('@/assets/partner/partner1l.png') },
                            { name: '海信', imgSrc: require('@/assets/partner/partner2l.png') },
                            { name: '电建', imgSrc: require('@/assets/partner/partner3l.png') },
                            { name: '好品', imgSrc: require('@/assets/partner/partner4l.png') }
                        ]
                    },
                    {
                        title: '金融行业',
                        content: '这里是金融行业介绍，这里是金融行业介绍，这里是金融行业相关介绍，这里是行业相关介绍，这里是行业相关介绍，这里是行业相关介绍。',
                        img: [
                            { name: '海尔', imgSrc: require('@/assets/partner/partner1l.png') },
                            { name: '海信', imgSrc: require('@/assets/partner/partner2l.png') },
                            { name: '电建', imgSrc: require('@/assets/partner/partner3l.png') },
                            { name: '好品', imgSrc: require('@/assets/partner/partner4l.png') }
                        ]
                    },
                    {
                        title: '金融行业',
                        content: '这里是金融行业介绍，这里是金融行业介绍，这里是金融行业相关介绍，这里是行业相关介绍，这里是行业相关介绍，这里是行业相关介绍。',
                        img: [
                            { name: '海尔', imgSrc: require('@/assets/partner/partner1l.png') },
                            { name: '海信', imgSrc: require('@/assets/partner/partner2l.png') },
                            { name: '电建', imgSrc: require('@/assets/partner/partner3l.png') },
                            { name: '好品', imgSrc: require('@/assets/partner/partner4l.png') }
                        ]
                    },
                    {
                        title: '金融行业',
                        content: '这里是金融行业介绍，这里是金融行业介绍，这里是金融行业相关介绍，这里是行业相关介绍，这里是行业相关介绍，这里是行业相关介绍。',
                        img: [
                            { name: '海尔', imgSrc: require('@/assets/partner/partner1l.png') },
                            { name: '海信', imgSrc: require('@/assets/partner/partner2l.png') },
                            { name: '电建', imgSrc: require('@/assets/partner/partner3l.png') },
                            { name: '好品', imgSrc: require('@/assets/partner/partner4l.png') }
                        ]
                    },
                    {
                        title: '金融行业',
                        content: '这里是金融行业介绍，这里是金融行业介绍，这里是金融行业相关介绍，这里是行业相关介绍，这里是行业相关介绍，这里是行业相关介绍。',
                        img: [
                            { name: '海尔', imgSrc: require('@/assets/partner/partner1l.png') },
                            { name: '海信', imgSrc: require('@/assets/partner/partner2l.png') },
                            { name: '电建', imgSrc: require('@/assets/partner/partner3l.png') },
                            { name: '好品', imgSrc: require('@/assets/partner/partner4l.png') }
                        ]
                    },
                    // { name: '海尔', light: require('@/assets/partner/partner1l.png') },
                    // { name: '海信', light: require('@/assets/partner/partner2l.png') },
                    // { name: '电建', light: require('@/assets/partner/partner3l.png') },
                    // { name: '好品', light: require('@/assets/partner/partner4l.png') },
                    // { name: '联信', light: require('@/assets/partner/partner5l.png') },
                    // { name: '清算', light: require('@/assets/partner/partner6l.png') },
                    // { name: '日日顺', light: require('@/assets/partner/partner7l.png') },
                    // { name: '航空', light: require('@/assets/partner/partner8l.png') }
                ]
            }
        },
        methods: {
            //跳转
            goPage(name, query) {
                // this.$route.push({
                //     name: name,
                //     query: query
                // })
            },
            //方案鼠标滑过
            solutionEnter(index1, index2) {
                this.solutionIndex = '' + index1 + index2;
            },
            solutionLeave() {
                this.solutionIndex = '';
            }
        }
    }
</script>

<style lang="scss" scoped>
    .home-product {
        .home-product-box {
            display: flex;
            .home-product-item {
                width: 3.36rem;
                height: 5.2rem;
                background-position: center;
                background-repeat: no-repeat;
                &.productActive0:hover {
                    background-image: url("../../../assets/home/product0.png");
                }
                &.productActive1:hover {
                    background-image: url("../../../assets/home/product1.png");
                }
                &.productActive2:hover {
                    background-image: url("../../../assets/home/product2.png");
                }
                &.productActive3:hover {
                    background-image: url("../../../assets/home/product3.png");
                }
                &.productActive4:hover {
                    background-image: url("../../../assets/home/product4.png");
                }
            }
        }
    }
    .home-solution {
        .home-solution-box {
            display: flex;
            flex-wrap: wrap;
            width: 14.88rem;
            justify-content: space-between;
            margin: 0 auto;
            .home-solution-item {
                position: relative;
                width: 7.2rem;
                height: 3.2rem;
                border-radius: 6px;
                background-image: url('../../../assets/home/物联网未选中背景.png');
                &.home-solution-item0,&.home-solution-item1 {
                    margin-bottom: .4rem;
                }
                &:hover {
                    box-shadow: 0 0 .3rem #a1b4d7;
                }
                img {
                    position: absolute;
                    top: .97rem;
                    left: .82rem;
                    width: 1.38rem;
                    height: 1.26rem;
                }
                .solution-item-right {
                    padding: .75rem .45rem 0 0;
                    margin-left: 2.62rem;
                    font-size: 18px;
                    color: #fff;
                    transform: scale(1);
                    transition: .3s all;
                    &.solution-item-right-big {
                        transform: scale(1.05);
                    }
                    h3 {
                        font-size: 26px;
                        line-height: .44rem;
                        color: #fff;
                    }
                    p {
                        height: .88rem;
                        margin-bottom: .04rem;
                        line-height: .28rem;
                    }
                    span {
                        display: block;
                        width: 1.32rem;
                        height: .44rem;
                        border: 1px solid #fff;
                        border-radius: 6px;
                        text-align: center;
                        line-height: .44rem;
                        cursor: pointer;
                    }
                }
            }
        }
    }
    .home-cases {
        .home-cases-box {
            display: flex;
            flex-wrap: wrap;
            justify-content: space-between;
            .home-cases-item {
                position: relative;
                width: 5.44rem;
                height: 5.6rem;
                border-radius: 6px;
                padding: .4rem .48rem 0 .4rem;
                box-shadow: 0 0 .1rem #e3edff;
                transition: .3s all;
                overflow: hidden;
                &.cases-margin-b {
                    margin-bottom: .48rem;
                }
                &:hover {
                    box-shadow: 0 0 .3rem #e3edff;
                    .cases-item-line {
                        width: 100%;
                    }
                }
                .cases-item-industry {
                    position: relative;
                    padding-left: .18rem;
                    margin-bottom: .34rem;
                    line-height: 16px;
                    font-size: 16px;
                    color: #042259;
                    &::before {
                        content: '';
                        position: absolute;
                        top: 2px;
                        left: 0;
                        width: 2px;
                        height: .12rem;
                        background: #042259;
                    }
                }
                .case-item-main {
                    height: 1.58rem;
                    margin-bottom: .22rem;
                    h3 {
                        margin-bottom: .14rem;
                        font-size: .24rem;
                        line-height: .38rem;
                        color: #042259;
                    }
                    p {
                        font-size: 16px;
                        line-height: .26rem;
                        color: #2d3c59;
                    }
                }
                .cases-item-more {
                    display: block;
                    font-size: 16px;
                    line-height: 16px;
                    color: #073c9f;
                    cursor: pointer;
                    i {
                        display: inline-block;
                        width: .12rem;
                        height: .11rem;
                        margin-top: 2px;
                        background: url("../../../assets/home/more.png") center no-repeat;
                        background-size: 100%;
                    }
                }
                img {
                    display: block;
                    max-height: 2.75rem;
                    margin: 0 auto;
                }
                .cases-item-line {
                    position: absolute;
                    bottom: 0;
                    left: 0;
                    width: 0;
                    height: .1rem;
                    background: #073c9f;
                    transition: .3s all;
                }
                &:last-child {
                    .cases-item-industry {
                        margin-top: 16%;
                    }
                    .case-img {
                        display: flex;
                        img {
                            width: 33%;
                            height: 33%;
                        }
                    }
                }
            }
        }
    }
    .home-partner {
        .home-partner-box {
            h3,p {
                text-align: center;
            }
            h3 {
                font-size: 18px;
                line-height: 18px;
                color: #042259;
                margin-bottom: .24rem;
            }
            p {
                font-size: 16px;
                line-height: 16px;
                color: #2d3c59;
            }
            .partner-img {
                display: flex;
                justify-content: space-around;
                align-items: center;
                .partner-img-item {
                    width: 3rem;
                    height: 3rem;
                    display: flex;
                    align-items: center;
                    justify-content: center;
                    img {
                        max-width: 2.4rem;
                    }
                }
            }
        }
    }

    /*swiper左右按钮样式*/
    .swiper-button-prev,.swiper-button-next{
        width: 1.08rem;
        height: 1.08rem;
        top: 45%;
        background: url("../../../assets/home/r-on.png") center no-repeat;
    }
    .swiper-button-prev {
        background-image: url("../../../assets/home/l-on.png");
    }
    .swiper-button-prev.swiper-button-disabled, .swiper-button-next.swiper-button-disabled {
        opacity: 1;
        background-image: url("../../../assets/home/r.png");
    }
    .swiper-button-prev.swiper-button-disabled {
        background-image: url("../../../assets/home/l.png");
    }
</style>
<style>
    /*合作客户swiper分页选中样式*/
    .my-bullet-active-b {
        opacity: 1;
        transform: scale(1.5);
    }
</style>
