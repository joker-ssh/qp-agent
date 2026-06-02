<template>
  <main class="page-shell">
    <section class="hero">
      <div class="hero__content">
        <p class="eyebrow">新媒体 · 知识 IP · 直播商业化</p>
        <h1>韦秋萍</h1>
        <p class="subtitle">8 年运营经验｜新媒体公司运营总监｜从 0 到 1 的实战型操盘手</p>
        <p class="intro">
          擅长知识 IP 矩阵孵化、短视频内容策略、直播间转化、投流优化与团队管理，
          曾独立操盘演讲口才赛道头部 IP，并完成心理学垂类项目的快速变现闭环。
        </p>
        <div class="hero__actions">
          <a class="button button--primary" href="#highlights">查看亮点</a>
          <a class="button button--ghost" href="/resume.pdf" target="_blank" rel="noreferrer">下载简历</a>
        </div>
      </div>
      <aside class="hero__card" aria-label="核心数据">
        <div v-for="metric in metrics" :key="metric.label" class="metric">
          <strong>{{ metric.value }}</strong>
          <span>{{ metric.label }}</span>
        </div>
      </aside>
    </section>

    <section id="highlights" class="section">
      <div class="section__heading">
        <p class="eyebrow">Highlights</p>
        <h2>核心亮点</h2>
      </div>
      <div class="card-grid">
        <article v-for="item in highlights" :key="item.title" class="card">
          <span class="card__index">{{ item.index }}</span>
          <h3>{{ item.title }}</h3>
          <p>{{ item.description }}</p>
        </article>
      </div>
    </section>

    <section class="section section--split">
      <div class="section__heading">
        <p class="eyebrow">Experience</p>
        <h2>工作经历</h2>
      </div>
      <div class="timeline">
        <article v-for="job in jobs" :key="job.company" class="timeline__item">
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

    <section class="section">
      <div class="section__heading">
        <p class="eyebrow">Cases</p>
        <h2>代表项目</h2>
      </div>
      <div class="case-card">
        <div>
          <h3>心理学垂类 IP 从 0 到 1</h3>
          <p>
            独立完成选题、文案、拍摄、剪辑风格与转化路径设计，通过“短视频 → 低价课 →
            私域沉淀 → 高阶产品”的模型跑通自然流量变现。
          </p>
        </div>
        <ul>
          <li>4 个月内私域变现 100 万+</li>
          <li>80+ 条高质量短视频内容</li>
          <li>单条最高播放 300 万+</li>
          <li>累计自然播放破 2000 万</li>
        </ul>
      </div>
    </section>

    <footer class="footer">
      <p>韦秋萍 · 新媒体运营总监</p>
      <a href="mailto:1584432155@qq.com">1584432155@qq.com</a>
    </footer>
  </main>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      metrics: [
        { value: '2400万+', label: '全网矩阵粉丝' },
        { value: '50人+', label: '跨部门团队管理' },
        { value: '100万+', label: '单项目快速变现' },
        { value: '300人+', label: '线下大课交付' },
      ],
      highlights: [
        {
          index: '01',
          title: '头部知识 IP 孵化',
          description: '独立操盘演讲口才赛道头部 IP“梁宸瑜”，覆盖内容、直播、投放与产品交付全链路。',
        },
        {
          index: '02',
          title: '内容与投流一体化',
          description: '用数据反哺选题和脚本，结合千川、本地推等投放策略，持续优化进粉成本和转化效率。',
        },
        {
          index: '03',
          title: '直播间高转化操盘',
          description: '熟悉人货场排布、逐字稿打磨、逼单节奏与 GPM 提升，具备付费主播和主讲出镜经验。',
        },
        {
          index: '04',
          title: '团队体系复制',
          description: '搭建 SOP、培训体系和人才梯队，培养编导、主播、运营负责人，让团队能持续打胜仗。',
        },
      ],
      jobs: [
        {
          company: '广州梁宸瑜文化传播有限公司',
          role: '运营总监',
          period: '2019.11 - 至今',
          points: [
            '负责口才、心理学等知识 IP 的生命周期管理与商业化顶层设计。',
            '审批短视频脚本，统筹直播运营与付费投放，对粉丝增长、爆款率和 GMV 负责。',
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
}
</script>
