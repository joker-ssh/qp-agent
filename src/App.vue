<template>
  <main
    class="app-shell"
    :class="[`motion-${motionName}`, { 'is-turning': isTurning }]"
    :style="{ '--cursor-x': `${cursor.x}px`, '--cursor-y': `${cursor.y}px` }"
    @mousemove="handlePointerMove"
    @wheel.prevent="handleWheel"
    @touchstart.passive="handleTouchStart"
    @touchend.passive="handleTouchEnd"
  >
    <div class="background-grid"></div>
    <div class="grain"></div>
    <div class="ambient ambient--one"></div>
    <div class="ambient ambient--two"></div>
    <div class="cursor-glow"></div>

    <header class="quiet-header">
      <button type="button" class="brand-mark" @click="goTo(0)">个人 IP 操盘手</button>
      <p>梁宸瑜账号一手操盘｜公司运营总监</p>
    </header>

    <div class="stage">
      <section
        v-for="(section, index) in sections"
        :key="section.id"
        class="screen"
        :class="[`screen--${section.id}`, { 'is-active': activeIndex === index, 'is-prev': previousIndex === index }]"
      >
        <div class="screen__inner">
          <template v-if="section.id === 'hero'">
            <div class="hero-copy">
              <p class="kicker">核心 IP 项目</p>
              <h1>
                <span>梁宸瑜，</span>
                <span>我一手做起来的口才 IP。</span>
              </h1>
              <p class="lead">
                我曾是梁宸瑜账号的操盘手，也是公司运营总监。这个账号不是单纯“做内容”，而是从人设定位、
                短视频内容、直播转化、投放优化到团队协作，一整套增长系统被持续跑通。
              </p>
              <div class="hero-badges">
                <span>全网矩阵 2400 万+ 粉丝</span>
                <span>演讲口才赛道 TOP3</span>
                <span>50 人+团队统筹</span>
              </div>
            </div>

            <div class="ip-hero">
              <div class="ip-hero__beam"></div>
              <figure class="phone-card phone-card--primary">
                <img :src="asset('ip-cases/liangchenyu-account-light.webp')" alt="梁宸瑜账号主页截图" />
              </figure>
              <figure class="phone-card phone-card--secondary">
                <img :src="asset('ip-cases/liangchenyu-account-dark.webp')" alt="梁宸瑜账号数据截图" />
              </figure>
              <article class="floating-card">
                <strong>2400万+</strong>
                <span>从 IP 定位到内容商业化的全链路操盘结果</span>
              </article>
            </div>
          </template>

          <template v-else-if="section.id === 'system'">
            <div class="section-heading">
              <p class="kicker">操盘系统</p>
              <h2>
                <span>我做 IP，</span>
                <span>不是靠灵感，是靠系统。</span>
              </h2>
            </div>
            <div class="system-map">
              <article v-for="item in systems" :key="item.title" class="system-card">
                <span>{{ item.index }}</span>
                <h3>{{ item.title }}</h3>
                <p>{{ item.text }}</p>
              </article>
            </div>
          </template>

          <template v-else-if="section.id === 'result'">
            <div class="case-copy">
              <p class="kicker">跨赛道复制</p>
              <h2>
                <span>黄骐认知舱，</span>
                <span>验证我的 IP 方法论。</span>
              </h2>
              <p>
                在心理学垂类项目里，我从零启动内容方向，独立完成选题、文案、拍摄风格、剪辑节奏和转化路径设计。
                通过短视频引流、低价课承接和私域转化，快速跑出商业结果。
              </p>
            </div>
            <div class="result-grid">
              <article v-for="metric in metrics" :key="metric.label">
                <strong>{{ metric.value }}</strong>
                <span>{{ metric.label }}</span>
              </article>
            </div>
          </template>

          <template v-else-if="section.id === 'proof'">
            <div class="proof-title">
              <p class="kicker">作品证据</p>
              <h2>
                <span>账号、课程、私域，</span>
                <span>都是真实链路的一部分。</span>
              </h2>
            </div>
            <div class="proof-wall">
              <figure v-for="work in works" :key="work.src">
                <img :src="asset(work.src)" :alt="work.alt" />
                <figcaption>{{ work.caption }}</figcaption>
              </figure>
            </div>
          </template>

          <template v-else>
            <div class="director-card">
              <p class="kicker">运营总监能力</p>
              <h2>
                <span>我能做账号，</span>
                <span>也能带团队打仗。</span>
              </h2>
              <div class="director-list">
                <p>统筹剪辑、文案、摄影、直播运营等团队，建立 SOP 和内部培训机制。</p>
                <p>用复盘机制应对平台算法变化，持续优化爆款率、进粉成本和直播转化。</p>
                <p>既能做前台出镜和直播转化，也能做后台组织管理与业务协同。</p>
              </div>
            </div>
          </template>
        </div>
      </section>
    </div>

    <nav class="progress-nav" aria-label="页面章节">
      <button
        v-for="(section, index) in sections"
        :key="section.id"
        type="button"
        :class="{ active: activeIndex === index }"
        @click="goTo(index)"
      >
        {{ section.nav }}
      </button>
    </nav>

    <div class="page-count">
      <span>{{ currentPage }}</span>
      <i></i>
      <span>{{ totalPages }}</span>
    </div>
  </main>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      activeIndex: 0,
      previousIndex: null,
      isTurning: false,
      motionName: 'rise',
      touchStartY: 0,
      cursor: { x: 0, y: 0 },
      sections: [
        { id: 'hero', nav: '梁宸瑜' },
        { id: 'system', nav: '操盘系统' },
        { id: 'result', nav: '黄骐认知舱' },
        { id: 'proof', nav: '作品链路' },
        { id: 'director', nav: '总监能力' },
      ],
      systems: [
        {
          index: '01',
          title: '人设与赛道定位',
          text: '先确定 IP 该解决谁的问题、用什么人格表达、用什么内容建立长期信任。',
        },
        {
          index: '02',
          title: '内容与直播转化',
          text: '短视频负责制造信任和流量，直播间负责承接需求、完成转化和沉淀用户。',
        },
        {
          index: '03',
          title: '投放与私域闭环',
          text: '用数据反哺内容和投放策略，把流量成本、转化率和后端成交放在一起看。',
        },
        {
          index: '04',
          title: '团队与 SOP 复制',
          text: '把个人经验拆成流程、标准和培训，让团队能稳定产出，而不是靠单点能力。',
        },
      ],
      metrics: [
        { value: '100万+', label: '4 个月私域变现' },
        { value: '80+', label: '单人完成短视频' },
        { value: '300万+', label: '单条最高播放' },
        { value: '8000+', label: '私域好友沉淀' },
      ],
      works: [
        { src: 'ip-cases/liangchenyu-account-light.webp', alt: '梁宸瑜账号主页', caption: '梁宸瑜账号矩阵' },
        { src: 'ip-cases/psychology-course-poster.webp', alt: '心理学课程海报', caption: '课程产品转化' },
        { src: 'ip-cases/huangqi-content-grid.webp', alt: '黄骐认知舱内容矩阵', caption: '短视频内容矩阵' },
        { src: 'ip-cases/private-community.webp', alt: '私域社群截图', caption: '私域承接链路' },
      ],
    }
  },
  computed: {
    currentPage() {
      return String(this.activeIndex + 1).padStart(2, '0')
    },
    totalPages() {
      return String(this.sections.length).padStart(2, '0')
    },
  },
  mounted() {
    window.addEventListener('keydown', this.handleKeydown)
  },
  beforeUnmount() {
    window.removeEventListener('keydown', this.handleKeydown)
  },
  methods: {
    asset(path) {
      return `${import.meta.env.BASE_URL}${path}`
    },
    handlePointerMove(event) {
      this.cursor = { x: event.clientX, y: event.clientY }
    },
    handleWheel(event) {
      if (Math.abs(event.deltaY) < 18) return
      this.step(event.deltaY > 0 ? 1 : -1)
    },
    handleTouchStart(event) {
      this.touchStartY = event.changedTouches[0].clientY
    },
    handleTouchEnd(event) {
      const distance = this.touchStartY - event.changedTouches[0].clientY
      if (Math.abs(distance) > 42) this.step(distance > 0 ? 1 : -1)
    },
    handleKeydown(event) {
      if (['ArrowDown', 'PageDown', ' '].includes(event.key)) {
        event.preventDefault()
        this.step(1)
      }

      if (['ArrowUp', 'PageUp'].includes(event.key)) {
        event.preventDefault()
        this.step(-1)
      }
    },
    step(direction) {
      const nextIndex = Math.min(Math.max(this.activeIndex + direction, 0), this.sections.length - 1)
      this.goTo(nextIndex)
    },
    goTo(index) {
      if (index === this.activeIndex || this.isTurning) return

      const motions = ['rise', 'split', 'zoom', 'slide', 'soft']
      this.previousIndex = this.activeIndex
      this.motionName = motions[index % motions.length]
      this.isTurning = true
      this.activeIndex = index

      window.setTimeout(() => {
        this.previousIndex = null
        this.isTurning = false
      }, 980)
    },
  },
}
</script>
