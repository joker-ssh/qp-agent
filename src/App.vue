<template>
  <main
    class="site"
    :style="{ '--cursor-x': `${cursor.x}px`, '--cursor-y': `${cursor.y}px` }"
    @mousemove="handlePointerMove"
  >
    <div class="soft-light soft-light--left"></div>
    <div class="soft-light soft-light--right"></div>
    <div class="cursor-halo" aria-hidden="true"></div>

    <nav class="nav reveal">
      <a class="brand" href="#top">Wei Qiuping</a>
      <div class="nav__links">
        <a href="#profile">介绍</a>
        <a href="#proof">成果</a>
        <a href="#experience">经历</a>
      </div>
      <a class="nav__button" :href="resumeHref" target="_blank" rel="noreferrer">简历</a>
    </nav>

    <section id="top" class="hero">
      <div class="hero__copy reveal">
        <p class="eyebrow">New Media Operations Director</p>
        <h1>温柔而有力量的内容增长操盘手</h1>
        <p class="hero__lead">
          韦秋萍，8 年新媒体运营经验，长期负责知识 IP 孵化、短视频内容、直播商业化、
          付费投放与团队管理。她的优势，是把内容审美、业务结果和组织效率放在同一个系统里。
        </p>
        <div class="hero__actions">
          <a class="button button--primary" href="#proof">查看成果</a>
          <a class="button button--plain" href="mailto:1584432155@qq.com">邮件联系</a>
        </div>
      </div>

      <aside class="portrait-card reveal" aria-label="个人能力摘要">
        <div class="portrait-card__image">
          <img :src="assetUrl('/showcase/case-4.webp')" alt="韦秋萍相关课程作品海报" />
        </div>
        <div class="portrait-card__body">
          <span>运营总监 / IP 操盘手</span>
          <strong>内容、直播、投放、私域转化全链路</strong>
        </div>
      </aside>
    </section>

    <section class="metrics reveal" aria-label="核心数据">
      <article v-for="metric in displayMetrics" :key="metric.label" class="metric">
        <strong>{{ metric.display }}</strong>
        <span>{{ metric.label }}</span>
      </article>
    </section>

    <section id="profile" class="section profile">
      <div class="section__intro reveal">
        <p class="eyebrow">Profile</p>
        <h2>她不是只会做内容的人，而是能把内容变成业务的人。</h2>
      </div>
      <div class="profile__grid">
        <article v-for="item in highlights" :key="item.title" class="feature-card reveal">
          <span>{{ item.index }}</span>
          <h3>{{ item.title }}</h3>
          <p>{{ item.description }}</p>
        </article>
      </div>
    </section>

    <section id="proof" class="section proof">
      <div class="section__intro reveal">
        <p class="eyebrow">Selected Proof</p>
        <h2>一些能看见的作品与结果。</h2>
      </div>
      <div class="proof__layout">
        <article class="proof__story reveal">
          <p class="eyebrow">Case Study</p>
          <h3>心理学垂类 IP 从 0 到 1</h3>
          <p>
            独立完成选题、文案、拍摄、视觉风格与转化路径设计，用“短视频 → 低价课 →
            私域沉淀 → 高阶产品”的方式跑通自然流量变现。
          </p>
          <ul>
            <li>4 个月私域变现 100 万+</li>
            <li>80+ 条高质量短视频</li>
            <li>单条最高播放 300 万+</li>
            <li>累计自然播放 2000 万+</li>
          </ul>
        </article>

        <div class="gallery reveal">
          <figure v-for="image in proofImages" :key="image.src" class="gallery__item">
            <img :src="image.src" :alt="image.alt" />
            <figcaption>{{ image.caption }}</figcaption>
          </figure>
        </div>
      </div>
    </section>

    <section id="experience" class="section experience">
      <div class="section__intro reveal">
        <p class="eyebrow">Experience</p>
        <h2>既能搭体系，也能亲自下场。</h2>
      </div>
      <div class="timeline">
        <article v-for="job in jobs" :key="job.company" class="timeline-card reveal">
          <div>
            <span>{{ job.period }}</span>
            <h3>{{ job.company }}</h3>
            <p>{{ job.role }}</p>
          </div>
          <ul>
            <li v-for="point in job.points" :key="point">{{ point }}</li>
          </ul>
        </article>
      </div>
    </section>

    <section class="closing reveal">
      <p class="eyebrow">Personal Website</p>
      <h2>适合展示给合作方、招聘方，也适合作为长期个人品牌入口。</h2>
      <div class="hero__actions">
        <a class="button button--primary" :href="resumeHref" target="_blank" rel="noreferrer">查看完整简历</a>
        <a class="button button--plain" href="mailto:1584432155@qq.com">1584432155@qq.com</a>
      </div>
    </section>
  </main>
</template>

<script>
const publicUrl = (path) => `${import.meta.env.BASE_URL}${path.replace(/^\//, '')}`

export default {
  name: 'App',
  data() {
    return {
      cursor: { x: 0, y: 0 },
      resumeHref: publicUrl('resume.pdf'),
      metricValues: [
        { value: 2400, suffix: '万+', label: '全网矩阵粉丝' },
        { value: 50, suffix: '人+', label: '跨部门团队管理' },
        { value: 100, suffix: '万+', label: '单项目快速变现' },
        { value: 300, suffix: '人+', label: '线下大课交付' },
      ],
      displayMetrics: [],
      proofImages: [
        { src: publicUrl('/showcase/case-1.webp'), alt: '账号主页截图', caption: '账号矩阵' },
        { src: publicUrl('/showcase/case-3.webp'), alt: '直播课程截图', caption: '课程转化' },
        { src: publicUrl('/showcase/case-5.webp'), alt: '视频内容列表截图', caption: '内容矩阵' },
        { src: publicUrl('/showcase/case-7.webp'), alt: '社群截图', caption: '私域承接' },
      ],
      highlights: [
        {
          index: '01',
          title: '知识 IP 孵化',
          description: '独立操盘演讲口才赛道头部 IP，覆盖内容、直播、投放和交付，不停留在管理表面。',
        },
        {
          index: '02',
          title: '内容商业化',
          description: '能把用户痛点、脚本表达、直播转化和投放数据连起来，用结果验证内容价值。',
        },
        {
          index: '03',
          title: '团队管理',
          description: '直管 50 人+中台团队，建立 SOP、培训体系和人才梯队，提升内容产出效率。',
        },
        {
          index: '04',
          title: '交付表达',
          description: '具备出镜导师、付费主播和线下大课交付经验，能面对用户，也能面对业务目标。',
        },
      ],
      jobs: [
        {
          company: '广州梁宸瑜文化传播有限公司',
          role: '运营总监',
          period: '2019.11 - 至今',
          points: [
            '负责口才、心理学等知识 IP 的生命周期管理与商业化顶层设计。',
            '统筹短视频内容、直播运营与付费投放，对粉丝增长、爆款率和 GMV 负责。',
            '直管 50 人+中台团队，建立跨部门 SOP 与内部培训体系。',
          ],
        },
        {
          company: '黄骐老师认知舱',
          role: '操盘手 / 出镜导师',
          period: '2025.12 - 2026.04',
          points: [
            '跨赛道操盘心理学 IP，仅 3 个月实现单号变现 100 万+。',
            '担任核心 IP 出镜导师与付费主播，负责高优场次直播转化。',
            '完成 300 人+线下大课交付，打通线上流量到线下高客单转化。',
          ],
        },
      ],
    }
  },
  mounted() {
    this.displayMetrics = this.metricValues.map((metric) => ({ ...metric, display: `0${metric.suffix}` }))
    this.setupReveal()
    this.animateMetrics()
  },
  methods: {
    assetUrl(path) {
      return publicUrl(path)
    },
    handlePointerMove(event) {
      this.cursor = { x: event.clientX, y: event.clientY }
    },
    setupReveal() {
      const observer = new IntersectionObserver(
        (entries) => {
          entries.forEach((entry) => {
            if (entry.isIntersecting) {
              entry.target.classList.add('is-visible')
            }
          })
        },
        { threshold: 0.16 },
      )

      document.querySelectorAll('.reveal').forEach((element) => observer.observe(element))
    },
    animateMetrics() {
      const duration = 1200
      const start = performance.now()

      const tick = (now) => {
        const progress = Math.min((now - start) / duration, 1)
        const eased = 1 - Math.pow(1 - progress, 3)

        this.displayMetrics = this.metricValues.map((metric) => ({
          ...metric,
          display: `${Math.round(metric.value * eased)}${metric.suffix}`,
        }))

        if (progress < 1) {
          requestAnimationFrame(tick)
        }
      }

      requestAnimationFrame(tick)
    },
  },
}
</script>
