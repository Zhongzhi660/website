# 论文结果展示设计说明

本页说明如何用当前组件更好地在网页上展示论文结果。

## 1. 页面结构建议

推荐顺序：

1. **Hero** — 标题、一句话贡献、Paper/Code/Dataset/Demo 入口  
2. **摘要 (TL;DR)** — 2–3 段概括，用 `Section variant="alt"`  
3. **研究动机** — 问题与动机，配图可用 `FigureWithCaption`  
4. **方法** — 方法描述 + **方法概览图**（大图用 `FigureWithCaption` + `wide`）  
5. **主要结果** — **关键数字**（`KeyResults`）+ **主表**（`ResultsTable`）+ 可选多图  
6. **引用 (Citation)** — 用 `Section variant="dark"` 收尾  

## 2. 核心结果怎么展示

### 2.1 用数字卡片突出 2–4 个结论

在「主要结果」区块顶部放 **KeyResults**，让读者一眼看到：

- 数据量减少倍数、性能提升百分比、FAC 覆盖率等

```astro
<KeyResults
  items={[
    { label: "数据量减少", value: "10×", desc: "在相同性能下" },
    { label: "性能提升", value: "+2.1%", desc: "vs 大规模合成" },
  ]}
/>
```

### 2.2 用表格展示主实验

用 **ResultsTable** 包一层，表格内对「Ours」行加 `class="highlight"`，自动高亮：

```astro
<ResultsTable>
  <table>
    <thead><tr><th>方法</th><th>准确率</th></tr></thead>
    <tbody>
      <tr><td>Baseline</td><td>72.1</td></tr>
      <tr class="highlight"><td><strong>Ours (FAC)</strong></td><td><strong>74.2</strong></td></tr>
    </tbody>
  </table>
</ResultsTable>
```

### 2.3 用图+标题展示方法/实验图

- **单图**：`<FigureWithCaption src="/figures/overview.png" caption="方法概览" />`  
- **大图全宽**：加 `wide`，`<FigureWithCaption ... wide />`  
- **多图并排**：  
  `figures={[{ src: "/figures/a.png", caption: "图 (a)" }, { src: "/figures/b.png", caption: "图 (b)" }]}`  

图片请放在 `public/figures/`，路径用 `/figures/xxx.png`。

## 3. Section 用法

- **variant="default"** — 白底  
- **variant="alt"** — 浅灰，用于摘要、方法等交替背景  
- **variant="dark"** — 深色，用于 Citation  
- **wide** — 内容区加宽（如 `wide`），适合大图或宽表  

## 4. 信息层次建议

- 首屏：标题 + 一句话贡献 + 四个按钮（Paper / Code / Dataset / Demo）  
- 每个 Section 一个主题，标题清晰（摘要、动机、方法、主要结果、引用）  
- 结果区：先 2–4 个数字卡片，再主表，再配图或消融表  
- 深色 Citation 区块作为明确收尾，方便复制 BibTeX  

按上述结构使用现有组件即可系统性地展示论文结果；具体数字与图片替换为你的实验内容即可。
