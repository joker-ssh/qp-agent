<template>
  <main
    class="site"
    :style="{ '--cursor-x': `${cursor.x}px`, '--cursor-y': `${cursor.y}px`, '--scroll-progress': `${scrollProgress}%` }"
    @mousemove="handlePointerMove"
  >
    <div class="background-grid"></div>
    <div class="grain"></div>
    <div class="cursor-glow"></div>

    <header class="top-shell">
      <button class="brand-mark" type="button" @click="scrollToSection('hero')">韦秋萍</button>
      <p>运营总监｜知识 IP 增长｜商业转化｜团队管理</p>
    </header>

    <nav class="side-progress" aria-label="页面章节">
      <a
        v-for="section in sections"
        :key="section.id"
        :href="`#${section.id}`"
        :class="{ active: activeSection === section.id }"
        @click.prevent="navigateToSection(section.id)"
      >
        <i></i>
        <span>{{ section.nav }}</span>
      </a>
    </nav>

    <section id="hero" class="scene scene--hero" data-scene>
      <div class="hero-copy reveal">
        <p class="kicker">面试展示 · 核心项目</p>
        <h1>
          <span>把知识付费赛道做成长期主义的人。</span>
        </h1>
        <p class="lead">
          目前担任运营总监，主要围绕梁宸瑜 IP 推进内容增长、直播转化、投放优化和团队协同。
          我关注的不只是单次曝光，而是账号能否形成清晰的商业路径、稳定的团队执行和可复盘的增长节奏。
        </p>
        <div class="hero-badges">
          <span>梁宸瑜 IP 重点参与操盘</span>
          <span>全网矩阵 2400 万+ 粉丝</span>
          <span>50 人团队协同管理</span>
        </div>
      </div>

      <div class="hero-visual reveal">
        <article class="result-chip">
          <strong>梁宸瑜 IP</strong>
          <span>演讲口才、销售口才、招商演讲赛道，知识付费商业 IP 操盘项目。</span>
        </article>
        <div class="hero-gallery">
          <figure
            v-for="(image, index) in heroImages"
            :key="image.src"
            :class="['phone-card', `phone-card--${index + 1}`]"
            @click="openImage(image, heroImages)"
          >
            <img :src="asset(displaySrc(image))" :alt="image.alt" :loading="index === 0 ? 'eager' : 'lazy'" decoding="async" />
          </figure>
        </div>
      </div>
    </section>

    <section id="core" class="scene scene--core" data-scene>
      <div class="section-heading reveal">
        <p class="kicker">核心能力结构</p>
        <h2>我的核心工作，围绕增长、转化和团队执行形成闭环。</h2>
      </div>

      <div class="core-index reveal">
        <article v-for="block in workBlocks" :key="block.id">
          <span>{{ block.index }}</span>
          <strong>{{ block.title }}</strong>
          <h3>{{ block.shortTitle }}</h3>
          <p>{{ block.text }}</p>
          <div>
            <i v-for="point in block.points" :key="point">{{ point }}</i>
          </div>
        </article>
      </div>
    </section>

    <section id="ip-growth" class="scene scene--work scene--ip" data-scene>
      <div class="work-copy reveal">
        <p class="kicker">01 · IP 增长</p>
        <h2>在成熟知识 IP 中，推进账号增长和内容矩阵升级。</h2>
        <p>
          梁宸瑜 IP 是我重点参与操盘的项目。我的工作覆盖内容增长、直播转化、投放优化和团队协同，
          重点是把账号结果背后的动作拆清楚、跑稳定、能复盘。
        </p>
      </div>

      <div class="ip-showcase reveal">
        <div class="wide-stage">
          <button type="button" class="stage-image" @click="openImage(ipFeatured, [ipFeatured])">
            <img :src="asset(displaySrc(ipFeatured))" :alt="ipFeatured.alt" loading="lazy" decoding="async" />
            <span>账号结果证据</span>
          </button>
          <div class="stage-side">
            <div class="stage-copy">
              <strong>从账号表现，回到可执行的增长动作</strong>
              <p>用内容节奏、直播承接、投放复盘和团队排班，把增长目标拆到每天可以执行、每周可以复盘的节点。</p>
            </div>
            <div class="media-strip media-strip--inline" aria-label="IP 增长视频素材">
              <button v-for="item in ipMedia" :key="item.src" type="button" @click="openMedia(item)">
                <video
                  :data-src="asset(item.src)"
                  muted
                  playsinline
                  loop
                  controls
                  preload="metadata"
                  data-autoplay
                ></video>
                <span>{{ item.caption }}</span>
              </button>
            </div>
          </div>
        </div>

        <div class="proof-groups" aria-label="IP 增长完整图片资料">
          <section v-for="group in ipProofGroups" :key="group.title" :class="['proof-group', `proof-group--${group.variant}`]">
            <div class="proof-group__head">
              <span>{{ group.title }}</span>
              <p>{{ group.text }}</p>
            </div>
            <div class="proof-cluster">
              <button
                v-for="item in group.items"
                :key="item.src"
                type="button"
                :class="orientationClass(item)"
                @click="openImage(item, group.items)"
              >
                <img :src="asset(displaySrc(item))" :alt="item.alt" loading="lazy" decoding="async" />
                <span>{{ item.caption }}</span>
              </button>
            </div>
          </section>
        </div>
      </div>
    </section>

    <section id="conversion" class="scene scene--conversion" data-scene>
      <div class="conversion-layout">
        <div class="work-copy reveal">
          <p class="kicker">02 · 商业转化</p>
          <h2>让内容不止停留在流量，而是进入可成交的链路。</h2>
          <p>
            我会从用户需求、内容信任、直播承接到私域跟进拆解路径，判断每个环节是否真的服务成交。
            对业务负责人来说，运营的价值不只是热度，而是能否把流量转成可持续的商业结果。
          </p>
        </div>
        <div class="conversion-flow reveal">
          <article v-for="step in conversionSteps" :key="step.title">
            <span>{{ step.index }}</span>
            <h3>{{ step.title }}</h3>
            <p>{{ step.text }}</p>
          </article>
        </div>
      </div>
    </section>

    <section id="team-sop" class="scene scene--work scene--sop" data-scene>
      <div class="work-copy reveal">
        <p class="kicker">03 · 团队 SOP</p>
        <h2>用 SOP 降低执行波动，让团队稳定产出。</h2>
        <p>团队管理上，我重视流程、培训、复盘和负责人梯队，让内容和直播动作不依赖某一个人临场发挥。</p>
      </div>
      <button class="sop-board reveal" type="button" @click="openImage(sopImage, [sopImage])">
        <img :src="asset(displaySrc(sopImage))" :alt="sopImage.alt" loading="lazy" decoding="async" />
        <span>查看 SOP 大图</span>
      </button>
    </section>

    <section id="trainer" class="scene scene--work scene--trainer" data-scene>
      <div class="work-copy reveal">
        <p class="kicker">04 · 讲师</p>
        <h2>把方法讲清楚，也把团队带到同一套标准里。</h2>
        <p>讲师经历体现的是表达、控场、培训和知识拆解能力。它能帮助团队理解为什么这样做，也知道具体怎么做。</p>
      </div>
      <div class="trainer-stage reveal">
        <video
          :data-src="asset(trainerVideo.src)"
          controls
          muted
          playsinline
          loop
          preload="metadata"
          data-autoplay
        ></video>
        <div class="trainer-gallery">
          <button
            v-for="item in trainerImages"
            :key="item.src"
            type="button"
            :class="orientationClass(item)"
            @click="openImage(item, trainerImages)"
          >
            <img :src="asset(displaySrc(item))" :alt="item.alt" loading="lazy" decoding="async" />
          </button>
        </div>
      </div>
    </section>

    <section id="anchor" class="scene scene--work scene--anchor" data-scene>
      <div class="work-copy reveal">
        <p class="kicker">05 · 主播</p>
        <h2>理解直播一线，才能更准确地管理直播结果。</h2>
        <p>主播相关素材以效果展示为主：大图体现现场状态，小图补充不同角度，展示镜头表达、场景适配和执行稳定性。</p>
      </div>
      <div class="anchor-wall reveal">
        <button
          v-for="item in anchorImages"
          :key="item.src"
          type="button"
          :class="orientationClass(item)"
          @click="openImage(item, anchorImages)"
        >
          <img :src="asset(displaySrc(item))" :alt="item.alt" loading="lazy" decoding="async" />
        </button>
      </div>
    </section>

    <section id="management" class="scene scene--management" data-scene>
      <div class="management-card reveal">
        <p class="kicker">适配岗位 · 结尾</p>
        <h2>我适合承担需要结果意识和组织能力的运营岗位。</h2>
        <div class="management-grid">
          <p>账号有内容基础，但商业化路径还不够清晰，需要有人把内容、直播、投放和私域串成闭环。</p>
          <p>团队能执行，但缺少稳定 SOP、复盘机制和负责人梯队，需要有人把经验沉淀成标准。</p>
          <p>老板希望运营负责人既懂内容，也能对结果、成本和团队效率负责。</p>
        </div>
        <div class="final-actions">
          <a :href="asset('content/resume/wei-qiuping-resume.pdf')" download>下载完整简历</a>
          <button type="button" @click="showContact = true">查看联系方式</button>
        </div>
      </div>
    </section>

    <div v-if="selectedMedia" class="modal" @click.self="closeMedia">
      <button class="modal__close" type="button" @click="closeMedia">关闭</button>
      <button v-if="canFlipMedia" class="modal__nav modal__nav--prev" type="button" @click="showPreviousMedia">上一张</button>
      <button v-if="canFlipMedia" class="modal__nav modal__nav--next" type="button" @click="showNextMedia">下一张</button>
      <figure class="modal__image">
        <video v-if="selectedMedia.type === 'video'" :src="asset(selectedMedia.src)" controls autoplay playsinline></video>
        <img v-else :src="asset(selectedMedia.src)" :alt="selectedMedia.alt" />
        <figcaption>{{ selectedMedia.caption || selectedMedia.alt }}</figcaption>
      </figure>
    </div>

    <div v-if="showContact" class="modal" @click.self="showContact = false">
      <section class="contact-card">
        <button class="modal__close" type="button" @click="showContact = false">关闭</button>
        <p class="kicker">联系方式</p>
        <h2>韦秋萍</h2>
        <a href="tel:18060751503" class="contact-link">电话：18060751503</a>
        <a href="mailto:1584432155@qq.com" class="contact-link">邮箱：1584432155@qq.com</a>
        <a :href="asset('content/resume/wei-qiuping-resume.pdf')" download class="contact-link">下载完整简历</a>
      </section>
    </div>
  </main>
</template>

<script>
const corePath = 'content/core-work'

export default {
  name: 'App',
  data() {
    return {
      activeSection: 'hero',
      scrollProgress: 0,
      cursor: { x: 0, y: 0 },
      selectedMedia: null,
      selectedMediaList: [],
      selectedMediaIndex: 0,
      showContact: false,
      sections: [
        { id: 'hero', nav: '首页' },
        { id: 'core', nav: '五大板块' },
        { id: 'ip-growth', nav: 'IP 增长' },
        { id: 'conversion', nav: '商业转化' },
        { id: 'team-sop', nav: '团队 SOP' },
        { id: 'trainer', nav: '讲师' },
        { id: 'anchor', nav: '主播' },
        { id: 'management', nav: '结尾' },
      ],
      heroImages: [
        { src: 'content/hero/微信图片_20260603104101_44698_12.png', thumb: 'content/optimized/hero-1.webp', alt: '梁宸瑜账号数据', caption: '账号数据' },
        { src: 'content/hero/微信图片_20260603104119_44699_12.png', thumb: 'content/optimized/hero-2.webp', alt: '梁宸瑜账号主页', caption: '账号主页' },
        { src: 'content/hero/微信图片_20260603104120_44700_12.png', thumb: 'content/optimized/hero-3.webp', alt: '梁宸瑜账号矩阵', caption: '账号矩阵' },
      ],
      workBlocks: [
        {
          id: 'ip-growth',
          index: '01',
          title: 'IP 增长',
          shortTitle: '让账号增长有节奏',
          headline: '从账号结果出发，把内容增长、直播转化、投放优化和团队协同放在一条线上看。',
          text: '梁宸瑜 IP 是我重点参与操盘的项目，覆盖内容增长、直播转化、投放优化和团队协同。',
          points: ['账号阶段判断', '内容矩阵规划', '直播转化承接', '投放复盘优化'],
        },
        {
          id: 'conversion',
          index: '02',
          title: '商业转化',
          shortTitle: '让流量进入成交',
          headline: '从流量到成交，先拆清楚用户路径，再安排内容和承接动作。',
          text: '商业转化关注的是内容信任、直播成交、私域跟进和交付质量，而不是只看播放量。',
          points: ['用户需求判断', '成交链路设计', '直播间节奏', '私域跟进复盘'],
        },
        {
          id: 'team-sop',
          index: '03',
          title: '团队 SOP',
          shortTitle: '让团队稳定执行',
          headline: '把经验变成流程，让团队稳定产出，而不是只靠个人灵感。',
          text: '通过 SOP、培训和复盘，把个人经验拆成团队可以持续执行的流程。',
          points: ['选题标准', '拍摄流程', '直播排班', '复盘机制'],
        },
        {
          id: 'trainer',
          index: '04',
          title: '讲师',
          shortTitle: '把方法讲清楚',
          headline: '把方法讲清楚，也把团队带进同一套执行标准。',
          text: '讲师工作体现的是表达、控场、培训和知识拆解能力。',
          points: ['现场表达', '方法拆解', '培训带教', '标准统一'],
        },
        {
          id: 'anchor',
          index: '05',
          title: '主播',
          shortTitle: '理解直播一线',
          headline: '亲自理解直播节奏，再反向优化团队标准。',
          text: '主播板块展示镜头状态、现场执行和不同场景下的表现稳定性。',
          points: ['镜头状态', '直播节奏', '场景适配', '表达稳定'],
        },
      ],
      ipFeatured: {
        src: `${corePath}/ip-growth/31191666776065_.pic.jpg`,
        thumb: 'content/optimized/ip-full-01.webp',
        alt: 'IP 增长账号结果',
        caption: '账号后台数据',
      },
      ipMedia: [
        { src: `${corePath}/ip-growth/95679_1663764541.mp4`, type: 'video', caption: '视频素材' },
        { src: `${corePath}/ip-growth/98992_1665320878.mp4`, type: 'video', caption: '直播片段' },
      ],
      ipProofImages: [
        { src: `${corePath}/ip-growth/31191666776065_.pic.jpg`, thumb: 'content/optimized/ip-full-01.webp', alt: '梁宸瑜视频号后台数据', caption: '梁宸瑜视频号后台' },
        { src: `${corePath}/ip-growth/31201666776097_.pic.jpg`, thumb: 'content/optimized/ip-full-02.webp', alt: '程程说话抖音后台数据', caption: '程程说话抖音后台' },
        { src: `${corePath}/ip-growth/31211666776125_.pic.jpg`, thumb: 'content/optimized/ip-full-03.webp', alt: '黄莉口才学堂视频号后台', caption: '黄莉口才学堂后台' },
        { src: `${corePath}/ip-growth/31221666776154_.pic.jpg`, thumb: 'content/optimized/ip-full-04.webp', alt: '张海涛讲表达后台数据', caption: '张海涛讲表达后台' },
        { src: `${corePath}/ip-growth/31231666776181_.pic.jpg`, thumb: 'content/optimized/ip-full-05.webp', alt: '商界演说家账号后台', caption: '商界演说家后台' },
        { src: `${corePath}/ip-growth/31241666776225_.pic.jpg`, thumb: 'content/optimized/ip-full-06.webp', alt: '抖音来客后台账号数据', caption: '抖音来客后台' },
        { src: `${corePath}/ip-growth/31251666776278_.pic.jpg`, thumb: 'content/optimized/ip-full-07.webp', alt: '抖音来客后台账号数据', caption: '抖音来客后台' },
        { src: `${corePath}/ip-growth/31261666776522_.pic.jpg`, thumb: 'content/optimized/ip-full-08.webp', alt: '抖音来客后台账号数据', caption: '抖音来客后台' },
        { src: `${corePath}/ip-growth/31271666776563_.pic.jpg`, thumb: 'content/optimized/ip-full-09.webp', alt: '抖音来客后台账号数据', caption: '抖音来客后台' },
        { src: `${corePath}/ip-growth/WechatIMG01215ad2fb41791c429603bc96dc599a.png`, thumb: 'content/optimized/ip-full-10.webp', alt: '直播间详情数据', caption: '直播间详情数据' },
        { src: `${corePath}/ip-growth/WechatIMG1a58d06920683e7880e20a1e0f2b69e7.png`, thumb: 'content/optimized/ip-full-11.webp', alt: '视频号助手数据大屏', caption: '视频号数据大屏' },
        { src: `${corePath}/ip-growth/WechatIMG35479.png`, thumb: 'content/optimized/ip-full-12.webp', orientation: 'portrait', alt: 'BOSS 直聘任职资料', caption: '任职资料' },
        { src: `${corePath}/ip-growth/WechatIMG448649416e23acd39466ef33e9bc6440.png`, thumb: 'content/optimized/ip-full-13.webp', alt: '直播数据趋势图', caption: '直播数据趋势' },
        { src: `${corePath}/ip-growth/WechatIMG4a410e3caa5f035258c639cc2f2c066b.png`, thumb: 'content/optimized/ip-full-14.webp', alt: '直播间详情数据', caption: '直播间详情数据' },
        { src: `${corePath}/ip-growth/WechatIMG96043.png`, thumb: 'content/optimized/ip-full-15.webp', orientation: 'portrait', alt: '梁宸瑜与马英夫妇账号截图', caption: '梁宸瑜与马英夫妇' },
        { src: `${corePath}/ip-growth/WechatIMG97235.png`, thumb: 'content/optimized/ip-full-16.webp', alt: '账号作品数据标注', caption: '作品数据标注' },
        { src: `${corePath}/ip-growth/WechatIMG97918.png`, thumb: 'content/optimized/ip-full-17.webp', alt: '直播复盘数据表', caption: '直播复盘表' },
        { src: `${corePath}/ip-growth/WechatIMG97924.png`, thumb: 'content/optimized/ip-full-18.webp', alt: '后台投放页面', caption: '投放后台页面' },
        { src: `${corePath}/ip-growth/WechatIMG98837.png`, thumb: 'content/optimized/ip-full-19.webp', alt: '账号作品数据标注', caption: '作品数据标注' },
        { src: `${corePath}/ip-growth/WechatIMG98838.png`, thumb: 'content/optimized/ip-full-20.webp', alt: '账号作品列表数据', caption: '作品列表数据' },
        { src: `${corePath}/ip-growth/WechatIMG98846.png`, thumb: 'content/optimized/ip-full-21.webp', alt: '账号作品数据标注', caption: '作品数据标注' },
        { src: `${corePath}/ip-growth/WechatIMG98848.png`, thumb: 'content/optimized/ip-full-22.webp', alt: '账号作品数据标注', caption: '作品数据标注' },
        { src: `${corePath}/ip-growth/WechatIMGb835b91f929f046f031c6cb7c71203f7.png`, thumb: 'content/optimized/ip-full-23.webp', alt: '视频号数据大屏', caption: '视频号数据大屏' },
        { src: `${corePath}/ip-growth/WechatIMGd3c20b781100aebd809dbebb50f16f58.png`, thumb: 'content/optimized/ip-full-24.webp', alt: '直播数据趋势图', caption: '直播数据趋势' },
        { src: `${corePath}/ip-growth/WechatIMGdb0d8b393e628d26e5676c8ee629a08c.png`, thumb: 'content/optimized/ip-full-25.webp', alt: '直播数据趋势图', caption: '直播数据趋势' },
        { src: `${corePath}/ip-growth/WechatIMGe462bd476589638e0f2c5c0dacf208b2.png`, thumb: 'content/optimized/ip-full-26.webp', alt: '直播间详情数据', caption: '直播间详情数据' },
      ],
      conversionSteps: [
        { index: '01', title: '先定目标', text: '明确账号阶段、收入目标、用户画像和团队资源，避免动作分散。' },
        { index: '02', title: '内容建信任', text: '用选题、脚本和表达风格让用户知道为什么要相信这个 IP。' },
        { index: '03', title: '直播做承接', text: '把短视频带来的兴趣承接到直播间节奏、话术和成交节点里。' },
        { index: '04', title: '私域做复盘', text: '看进粉成本、成交效率、服务反馈和利润空间，再调整下一轮打法。' },
      ],
      sopImage: {
        src: `${corePath}/team-sop/微信图片_20260603110121_44762_12.jpg`,
        thumb: 'content/optimized/sop.webp',
        alt: '团队 SOP 图片',
        caption: '团队 SOP 流程资料',
      },
      trainerVideo: {
        src: `${corePath}/trainer/a4557c63b3c546aa863882a83182be6a_raw.mp4`,
        type: 'video',
        caption: '讲师视频',
      },
      trainerImages: [
        { src: `${corePath}/trainer/微信图片_20260603110501_44765_12.jpg`, thumb: 'content/optimized/trainer-1.webp', alt: '讲师现场照片', caption: '讲师现场' },
        { src: `${corePath}/trainer/微信图片_20260603110503_44767_12.jpg`, thumb: 'content/optimized/trainer-2.webp', orientation: 'portrait', alt: '讲师展示照片', caption: '讲师展示' },
        { src: `${corePath}/trainer/微信图片_20260603110504_44768_12.jpg`, thumb: 'content/optimized/trainer-3.webp', orientation: 'portrait', alt: '讲师状态照片', caption: '讲师状态' },
      ],
      anchorImages: [
        { src: `${corePath}/anchor/微信图片_20260603110505_44770_12.jpg`, thumb: 'content/optimized/anchor-1.webp', alt: '主播场景照片', caption: '主播场景' },
        { src: `${corePath}/anchor/微信图片_20260603110507_44771_12.jpg`, thumb: 'content/optimized/anchor-2.webp', orientation: 'portrait', alt: '主播现场照片', caption: '主播现场' },
        { src: `${corePath}/anchor/微信图片_20260603110559_44774_12.jpg`, thumb: 'content/optimized/anchor-5.webp', orientation: 'portrait', alt: '主播展示截图', caption: '镜头状态' },
        { src: `${corePath}/anchor/微信图片_20260603110808_44777_12.jpg`, thumb: 'content/optimized/anchor-7.webp', orientation: 'portrait', alt: '主播展示截图', caption: '执行效果' },
        { src: `${corePath}/anchor/微信图片_20260603110558_44773_12.jpg`, thumb: 'content/optimized/anchor-4.webp', orientation: 'portrait', alt: '主播展示截图', caption: '直播状态' },
        { src: `${corePath}/anchor/微信图片_20260603110600_44775_12.jpg`, thumb: 'content/optimized/anchor-6.webp', orientation: 'portrait', alt: '主播展示截图', caption: '场景适配' },
        { src: `${corePath}/anchor/微信图片_20260603110557_44772_12.jpg`, thumb: 'content/optimized/anchor-3.webp', orientation: 'portrait', alt: '主播展示截图', caption: '主播展示' },
      ],
    }
  },
  computed: {
    ipProofGroups() {
      return [
        {
          title: '短视频账号与内容后台',
          variant: 'account',
          text: '账号主页、作品动态、内容矩阵和短视频平台后台相关截图。',
          items: [
            this.ipProofImages[0],
            this.ipProofImages[1],
            this.ipProofImages[2],
            this.ipProofImages[3],
            this.ipProofImages[4],
            this.ipProofImages[15],
            this.ipProofImages[18],
            this.ipProofImages[19],
            this.ipProofImages[20],
            this.ipProofImages[21],
            this.ipProofImages[5],
            this.ipProofImages[6],
            this.ipProofImages[7],
            this.ipProofImages[8],
          ],
        },
        {
          title: '直播投放与数据看板',
          variant: 'data',
          text: '直播数据、投放看板、经营数据和阶段复盘相关截图。',
          items: [
            this.ipProofImages[10],
            this.ipProofImages[22],
            this.ipProofImages[9],
            this.ipProofImages[13],
            this.ipProofImages[25],
            this.ipProofImages[12],
            this.ipProofImages[23],
            this.ipProofImages[24],
            this.ipProofImages[17],
            this.ipProofImages[16],
          ],
        },
        {
          title: '其他',
          variant: 'support',
          text: '任职信息和其他补充资料。',
          items: [
            this.ipProofImages[11],
            this.ipProofImages[14],
          ],
        },
      ]
    },
    canFlipMedia() {
      return this.selectedMediaList.length > 1
    },
  },
  mounted() {
    this.setupReveal()
    this.setupVideoObserver()
    window.addEventListener('scroll', this.handleScroll, { passive: true })
    window.addEventListener('hashchange', this.handleHashChange)
    this.handleScroll()
    requestAnimationFrame(this.handleScroll)
    window.setTimeout(this.handleScroll, 300)
    window.setTimeout(this.handleHashChange, 120)
  },
  beforeUnmount() {
    window.removeEventListener('scroll', this.handleScroll)
    window.removeEventListener('hashchange', this.handleHashChange)
  },
  methods: {
    asset(path) {
      return `${import.meta.env.BASE_URL}${path}`
    },
    displaySrc(item) {
      return item.thumb || item.src
    },
    orientationClass(item) {
      return item.orientation === 'portrait' ? 'is-portrait' : 'is-wide'
    },
    handlePointerMove(event) {
      this.cursor = { x: event.clientX, y: event.clientY }
    },
    handleScroll() {
      const maxScroll = document.documentElement.scrollHeight - window.innerHeight
      this.scrollProgress = maxScroll > 0 ? Math.min((window.scrollY / maxScroll) * 100, 100) : 0
      this.updateActiveSection()
    },
    navigateToSection(id) {
      history.pushState(null, '', `#${id}`)
      this.scrollToSection(id)
      window.setTimeout(this.handleScroll, 420)
    },
    scrollToSection(id, behavior = 'smooth') {
      const section = document.getElementById(id)
      if (!section) return
      const offset = Math.max((window.innerHeight - section.offsetHeight) / 2, 22)
      window.scrollTo({
        top: section.offsetTop - offset,
        behavior,
      })
    },
    handleHashChange() {
      const id = window.location.hash.replace('#', '')
      if (!id) return
      ;[80, 420, 1000, 1800].forEach((delay) => {
        window.setTimeout(() => {
          this.scrollToSection(id, 'auto')
          this.handleScroll()
        }, delay)
      })
    },
    openImage(image, list = []) {
      this.selectedMediaList = list.length ? list : [image]
      this.selectedMediaIndex = Math.max(
        this.selectedMediaList.findIndex((item) => item.src === image.src),
        0,
      )
      this.selectedMedia = { ...this.selectedMediaList[this.selectedMediaIndex], type: 'image' }
    },
    openMedia(media) {
      this.selectedMediaList = [media]
      this.selectedMediaIndex = 0
      this.selectedMedia = media.type === 'video' ? media : { ...media, type: 'image' }
    },
    showPreviousMedia() {
      if (!this.canFlipMedia) return
      this.selectedMediaIndex = (this.selectedMediaIndex - 1 + this.selectedMediaList.length) % this.selectedMediaList.length
      this.selectedMedia = { ...this.selectedMediaList[this.selectedMediaIndex], type: 'image' }
    },
    showNextMedia() {
      if (!this.canFlipMedia) return
      this.selectedMediaIndex = (this.selectedMediaIndex + 1) % this.selectedMediaList.length
      this.selectedMedia = { ...this.selectedMediaList[this.selectedMediaIndex], type: 'image' }
    },
    closeMedia() {
      this.selectedMedia = null
      this.selectedMediaList = []
      this.selectedMediaIndex = 0
    },
    setupReveal() {
      const observer = new IntersectionObserver(
        (entries) => {
          entries.forEach((entry) => {
            if (entry.isIntersecting) entry.target.classList.add('is-visible')
          })
        },
        { threshold: 0.14 },
      )

      document.querySelectorAll('.reveal').forEach((element) => observer.observe(element))
    },
    updateActiveSection() {
      const scenes = Array.from(document.querySelectorAll('[data-scene]'))
      const center = window.innerHeight * 0.42
      const current = scenes.find((scene) => {
        const rect = scene.getBoundingClientRect()
        return rect.top <= center && rect.bottom > center
      })
      if (current) this.activeSection = current.id
    },
    setupVideoObserver() {
      const observer = new IntersectionObserver(
        (entries) => {
          entries.forEach((entry) => {
            const video = entry.target
            if (entry.isIntersecting) {
              if (!video.getAttribute('src')) {
                video.setAttribute('src', video.dataset.src)
                video.load()
              }
              video.play().catch(() => {})
            } else {
              video.pause()
            }
          })
        },
        { threshold: 0.55 },
      )

      document.querySelectorAll('video[data-autoplay]').forEach((video) => observer.observe(video))
    },
  },
}
</script>
