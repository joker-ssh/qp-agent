<template>
  <main
    class="site"
    :style="{ '--cursor-x': `${cursor.x}px`, '--cursor-y': `${cursor.y}px`, '--scroll-progress': `${scrollProgress}%` }"
    @mousemove="handlePointerMove"
  >
    <div class="background-grid"></div>
    <div class="grain"></div>
    <div class="ambient ambient--one"></div>
    <div class="ambient ambient--two"></div>
    <div class="cursor-glow"></div>

    <header class="top-shell">
      <button class="brand-mark" type="button" @click="scrollToSection('hero')">韦秋萍</button>
      <p>运营总监｜梁宸瑜账号操盘手｜知识 IP 商业化</p>
    </header>

    <nav class="side-progress" aria-label="页面章节">
      <button
        v-for="section in sections"
        :key="section.id"
        type="button"
        :class="{ active: activeSection === section.id }"
        @click="scrollToSection(section.id)"
      >
        <i></i>
        <span>{{ section.nav }}</span>
      </button>
    </nav>

    <section id="hero" class="scene scene--hero" data-scene>
      <div class="hero-copy reveal">
              <p class="kicker">面试展示 · 核心项目</p>
              <h1>
                <span>韦秋萍</span>
                <span>把知识 IP 做成长期生意的人</span>
              </h1>
              <p class="lead">
          我目前担任运营总监，主要负责知识 IP 的内容增长、直播转化、投放优化和团队管理。
          梁宸瑜账号是我重点参与操盘的代表项目之一，也是我运营方法和团队管理能力的集中体现。
              </p>
        <div class="hero-badges">
          <span>梁宸瑜 IP 核心操盘</span>
          <span>全网矩阵 2400 万+ 粉丝</span>
          <span>50 人+团队统筹协作</span>
        </div>
      </div>

      <div class="hero-visual reveal">
        <div class="light-ring"></div>
              <figure class="phone-card phone-card--main" @click="openImage(heroImages[0])">
                <img :src="asset(heroImages[0].src)" :alt="heroImages[0].alt" />
              </figure>
        <figure class="phone-card phone-card--back" @click="openImage(heroImages[1])">
          <img :src="asset(heroImages[1].src)" :alt="heroImages[1].alt" />
        </figure>
              <article class="result-chip">
          <strong>梁宸瑜</strong>
          <span>我重点参与操盘的口才赛道知识 IP，全网矩阵粉丝 2400 万+</span>
              </article>
      </div>
    </section>

    <section id="overview" class="scene scene--overview" data-scene>
      <div class="section-heading reveal">
        <p class="kicker">核心履历概览</p>
        <h2>我做过的核心工作，主要集中在 IP 增长、商业转化和团队管理。</h2>
      </div>
      <div class="overview-grid">
        <article v-for="item in overview" :key="item.title" class="overview-card reveal">
          <span>{{ item.index }}</span>
          <h3>{{ item.title }}</h3>
          <p>{{ item.text }}</p>
        </article>
      </div>
    </section>

    <section id="system" class="scene scene--system" data-scene>
      <div class="sticky-layout">
        <div class="sticky-title reveal">
          <p class="kicker">我的工作方式</p>
          <h2>重视系统能力，也重视团队协作。</h2>
          <p>
            面对老板或业务负责人，我会先把目标、阶段、资源和风险拆清楚，再推进内容、直播、投放和团队协作。
            我不希望运营只靠个人灵感，而是希望团队能持续稳定地跑出结果。
          </p>
        </div>
        <div class="system-stack">
          <article v-for="item in systems" :key="item.title" class="system-card reveal">
            <span>{{ item.index }}</span>
            <h3>{{ item.title }}</h3>
            <p>{{ item.text }}</p>
          </article>
        </div>
      </div>
    </section>

    <section id="case" class="scene scene--case" data-scene>
      <div class="case-copy reveal">
        <p class="kicker">项目复用 · 黄骐认知舱</p>
        <h2>从成熟 IP 方法，到新的内容项目。</h2>
        <p>
          在心理学垂类项目中，我尝试把过往在知识 IP 中沉淀的方法复用到新赛道：先明确用户痛点和信任路径，
          再规划短视频内容、低价课承接和私域转化。这段经历让我更确信，运营不只是做爆款，而是把路径拆清楚、把结果复盘清楚。
        </p>
      </div>
      <div class="case-panel reveal">
        <button class="case-image" type="button" @click="openImage(caseImage)">
          <img :src="asset(caseImage.src)" :alt="caseImage.alt" />
          <span>点击查看原图</span>
        </button>
        <div class="case-result">
          <p class="case-result__label">阶段性结果</p>
          <div class="metrics">
            <article v-for="metric in metrics" :key="metric.label">
              <strong>{{ metric.value }}</strong>
              <span>{{ metric.label }}</span>
            </article>
          </div>
        </div>
      </div>
    </section>

    <section id="proof" class="scene scene--proof" data-scene>
      <div class="section-heading reveal">
        <p class="kicker">项目材料</p>
        <h2>账号、课程、内容、私域，共同构成完整运营链路。</h2>
      </div>
      <div class="proof-wall">
        <figure v-for="work in works" :key="work.src" class="reveal" @click="openImage(work)">
          <img :src="asset(work.src)" :alt="work.alt" />
          <figcaption>{{ work.caption }} · 点击放大</figcaption>
        </figure>
      </div>
    </section>

    <section id="management" class="scene scene--management" data-scene>
      <div class="management-card reveal">
        <p class="kicker">管理与协作</p>
        <h2>作为运营总监，我更看重团队一起赢。</h2>
        <div class="management-grid">
          <p>我负责统筹内容、剪辑、摄影、直播运营等团队，把目标拆到流程、节点和复盘机制里。</p>
          <p>面对平台变化和流量波动，我习惯用数据复盘，而不是简单归因，持续优化内容效率和转化效率。</p>
          <p>我可以亲自下场做内容和直播，也可以把经验沉淀成 SOP，帮助团队降低对个人经验的依赖。</p>
        </div>
        <div class="fit-list">
          <h3>我适合解决的问题</h3>
          <ul>
            <li>账号有内容基础，但商业化路径还不够清晰。</li>
            <li>团队能执行，但缺少稳定 SOP、复盘机制和负责人梯队。</li>
            <li>老板希望运营负责人既懂内容，也能对结果和团队效率负责。</li>
          </ul>
        </div>
        <div class="final-actions">
          <a :href="asset('content/resume/wei-qiuping-resume.pdf')" download>下载完整简历</a>
          <button type="button" @click="showContact = true">查看联系方式</button>
        </div>
      </div>
    </section>

    <div v-if="selectedImage" class="modal" @click.self="closeImage">
      <button class="modal__close" type="button" @click="closeImage">关闭</button>
      <figure class="modal__image">
        <img :src="asset(selectedImage.src)" :alt="selectedImage.alt" />
        <figcaption>{{ selectedImage.caption || selectedImage.alt }}</figcaption>
      </figure>
    </div>

    <div v-if="showContact" class="modal" @click.self="showContact = false">
      <section class="contact-card">
        <button class="modal__close" type="button" @click="showContact = false">关闭</button>
        <p class="kicker">联系方式</p>
        <h2>韦秋萍</h2>
        <a href="tel:1584432155" class="contact-link">电话：1584432155</a>
        <a href="mailto:1584432155@qq.com" class="contact-link">邮箱：1584432155@qq.com</a>
        <a :href="asset('content/resume/wei-qiuping-resume.pdf')" download class="contact-link">下载完整简历</a>
      </section>
    </div>
  </main>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      activeSection: 'hero',
      scrollProgress: 0,
      cursor: { x: 0, y: 0 },
      selectedImage: null,
      showContact: false,
      sections: [
        { id: 'hero', nav: '韦秋萍' },
        { id: 'overview', nav: '履历概览' },
        { id: 'system', nav: '工作方式' },
        { id: 'case', nav: '项目复用' },
        { id: 'proof', nav: '项目材料' },
        { id: 'management', nav: '管理协作' },
      ],
      heroImages: [
        { src: 'content/liangchenyu/account-home.png', alt: '梁宸瑜账号主页截图', caption: '梁宸瑜账号主页' },
        { src: 'content/liangchenyu/account-data.png', alt: '梁宸瑜账号成果截图', caption: '梁宸瑜账号成果' },
      ],
      caseImage: { src: 'content/huangqi/course-poster.jpg', alt: '心理学课程海报', caption: '心理学课程承接页面' },
      overview: [
        {
          index: '01',
          title: '负责过账号结果',
          text: '梁宸瑜 IP 是我重点参与操盘的项目，覆盖内容增长、直播转化、投放优化和团队协同。',
        },
        {
          index: '02',
          title: '理解老板关心的指标',
          text: '不只看播放量，也会看进粉成本、转化效率、团队人效、交付质量和利润空间。',
        },
        {
          index: '03',
          title: '能把经验交给团队',
          text: '通过 SOP、培训和复盘，把个人经验拆成团队可以持续执行的流程。',
        },
      ],
      systems: [
        {
          index: '01',
          title: '先理解业务目标',
          text: '确认账号阶段、商业目标、用户需求和团队资源，再决定内容重点，而不是单纯追热点或追播放量。',
        },
        {
          index: '02',
          title: '把内容和转化连起来',
          text: '短视频、直播间、投放和私域围绕同一条用户路径协同，避免各做各的。',
        },
        {
          index: '03',
          title: '用复盘降低不确定性',
          text: '把选题、脚本、完播、进粉成本、成交数据放在一起看，让调整有依据。',
        },
        {
          index: '04',
          title: '让团队稳定产出',
          text: '管理上重视 SOP、培训和梯队建设，让团队能力可以复制，避免业务依赖某一个人。',
        },
      ],
      metrics: [
        { value: '100万+', label: '心理学项目 4 个月私域变现' },
        { value: '80+', label: '单人阶段完成短视频内容' },
        { value: '300万+', label: '单条内容最高播放量' },
        { value: '8000+', label: '私域用户沉淀规模' },
      ],
      works: [
        { src: 'content/liangchenyu/account-home.png', alt: '梁宸瑜账号主页', caption: '梁宸瑜账号矩阵' },
        { src: 'content/huangqi/course-poster.jpg', alt: '心理学课程海报', caption: '课程产品承接' },
        { src: 'content/huangqi/content-grid.png', alt: '黄骐认知舱内容矩阵', caption: '短视频内容矩阵' },
        { src: 'content/private-domain/community.jpg', alt: '私域社群截图', caption: '私域承接链路' },
      ],
    }
  },
  mounted() {
    this.setupReveal()
    this.setupSceneObserver()
    window.addEventListener('scroll', this.handleScroll, { passive: true })
    this.handleScroll()
  },
  beforeUnmount() {
    window.removeEventListener('scroll', this.handleScroll)
  },
  methods: {
    asset(path) {
      return `${import.meta.env.BASE_URL}${path}`
    },
    handlePointerMove(event) {
      this.cursor = { x: event.clientX, y: event.clientY }
    },
    handleScroll() {
      const maxScroll = document.documentElement.scrollHeight - window.innerHeight
      this.scrollProgress = maxScroll > 0 ? Math.min((window.scrollY / maxScroll) * 100, 100) : 0
    },
    scrollToSection(id) {
      document.getElementById(id)?.scrollIntoView({ behavior: 'smooth', block: 'start' })
    },
    openImage(image) {
      this.selectedImage = image
    },
    closeImage() {
      this.selectedImage = null
    },
    setupReveal() {
      const observer = new IntersectionObserver(
        (entries) => {
          entries.forEach((entry) => {
            if (entry.isIntersecting) entry.target.classList.add('is-visible')
          })
        },
        { threshold: 0.18 },
      )

      document.querySelectorAll('.reveal').forEach((element) => observer.observe(element))
    },
    setupSceneObserver() {
      const observer = new IntersectionObserver(
        (entries) => {
          entries.forEach((entry) => {
            if (entry.isIntersecting) this.activeSection = entry.target.id
          })
        },
        { threshold: 0.45 },
      )

      document.querySelectorAll('[data-scene]').forEach((scene) => observer.observe(scene))
    },
  },
}
</script>
