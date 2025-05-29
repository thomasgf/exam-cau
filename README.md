# 📄 `exam-cau.cls` 使用说明书

> 中国农业大学考试试卷模板
>

本模板 `exam-cau.cls` 是为中国农业大学设计的 LaTeX 考试试卷排版类文件。支持：

- 多平台字体自动适配（MacOS / Windows / Linux）
- 题目编号与表格自动生成
- 答案显示控制（开关式）
- 自定义年份、科目、学期信息
- 支持选择题、填空题、计算题等常见题型

---

## ⚙️ 1. 使用前提条件

### ✅ 必须安装的宏包（建议使用 TeX Live 或 MiKTeX）

```latex
xcolor, environ,
amsmath, amsthm, amssymb, amsfonts,
fontspec, graphicx, color, setspace,
fancyhdr, float, bm, xparse, array, etoolbox

```

> ✅ 编译方式推荐：XeLaTeX
>

---

## 🧱 2. 类选项说明（可选参数）

在 `\\documentclass` 中可以传入以下操作系统选项以适配不同系统下的中文字体：

| 参数 | 含义 |
| --- | --- |
| `macos` | 使用 MacOS 字体（默认） |
| `windows` | 使用 Windows 常见中文字体（如宋体、黑体） |
| `linux` | 使用 Linux 下常见字体（如文泉驿正黑） |

示例：

```latex
\\documentclass[macos]{exam-cau}

```

> ⚠️ 如果不指定，默认为 macos，可根据需要修改 .cls 文件中的默认值。
>

---

## 📌 3. 主要命令说明

### 🔹 设置考试基本信息

| 命令 | 功能 | 示例 |
| --- | --- | --- |
| `\\setyear{<年份>}` | 设置考试年份 | `\\setyear{2025}` |
| `\\setsubject{<科目名>}` | 设置考试科目 | `\\setsubject{高等数学}` |
| `\\setsemester{<学期>}` | 设置考试学期 | `\\setsemester{春季学期}` |

---

### 🔹 控制答案是否显示（调试/打印用）

| 命令 | 功能 | 示例 |
| --- | --- | --- |
| `\\includeanswertrue` | 显示答案 | `\\includeanswertrue` |
| `\\includeanswerfalse` | 不显示答案（默认） | `\\includeanswerfalse` |

---

### 🔹 添加题目内容

```latex
\\problem{<分数>}{<题型标题>}{<题目内容>}

```

- `<分数>`：每道大题的总分
- `<题型标题>`：如“选择题”、“填空题”、“计算题”
- `<题目内容>`：具体题目正文，可包含 `enumerate` 列表、公式环境等

✅ 示例：

```latex
\\problem{12}{选择题}{
  \\begin{enumerate}
    \\item 函数 $ f(x) = |x| $ 在 $ x=0 $ 处：
      \\begin{answer}
        不可导
      \\end{answer}
  \\end{enumerate}
}

```

---

### 🔹 插入答案（配合 `\\includeanswertrue`）

```latex
\\begin{answer}
  正确答案或参考解答
\\end{answer}

```

- 使用 `\\includeanswertrue` 可显示答案区域
- 使用 `\\includeanswerfalse` 或省略该命令则隐藏答案

---

### 🔹 生成试卷标题和题目表格

```latex
\\generateExamTitle   % 输出试卷头部信息
\\generateProblemTable % 输出题目列表表格 + 所有题目的正文

```

---

## 📋 4. 表格样式说明

| 表头 | 内容 |
| --- | --- |
| 第一行 | 题号（一、二、三...） |
| 第二行 | 分数占位符（空白单元格） |
| 第三行 | 总分列 |

---

## 🧾 5. 完整示例文档 (`main.tex`)

```latex
\\documentclass[windows]{exam-cau}

% 控制是否显示答案
\\includeanswertrue   % 显示答案
%\\includeanswerfalse  % 不显示答案

\\begin{document}

% 考试信息设置
\\setyear{2025}
\\setsubject{高等数学}
\\setsemester{春季学期}

% 生成试卷标题
\\generateExamTitle

% 添加题目
\\problem{12}{选择题}{
  \\begin{enumerate}
    \\item 函数 $ f(x) = |x| $ 在 $ x=0 $ 处：
      \\begin{answer}
        不可导
      \\end{answer}
    \\item 若 $ f(x) = e^{2x} $，则 $ f'(x) = $ ?
      \\begin{answer}
        $ 2e^{2x} $
      \\end{answer}
  \\end{enumerate}
}

\\problem{8}{计算题}{
  计算极限：
  $$
  \\lim_{x \\to 0} \\frac{\\sin 2x}{x}
  $$
  \\begin{answer}
    $$
    \\lim_{x \\to 0} \\frac{\\sin 2x}{x}
    = \\lim_{x \\to 0} 2 \\cdot \\frac{\\sin 2x}{2x}
    = 2 \\cdot 1 = 2
    $$
  \\end{answer}
}

% 输出表格和正文
\\generateProblemTable

\\end{document}

```

---

## 🎨 6. 答案格式说明

- 答案部分用红色加粗显示“【参考答案】”
- 答案正文为蓝色字体
- 默认不显示答案（更适用于打印试卷）

---

## 🛠️ 7. 已知功能与扩展建议

### ✅ 当前已实现功能

- 自动题号生成
- 表格自动对齐
- 答案显示控制
- 多平台字体适配
- 页眉页脚定制
- 诚信承诺栏
- 标题栏美观排版

### 💡 可扩展建议（后续可添加）

| 功能 | 描述 |
| --- | --- |
| `\\scoreline` | 自动生成得分栏 |
| `\\answerpage` | 单独输出所有答案一页 |
| `\\useanswersheettrue` | 开启答题本模式（仅留空题） |
| `\\zihao` 字号调整 | 更精细控制字体大小 |
| `\\makecell` 美化表格 | 支持换行、居中 |
| `\\boxed` | 数学公式答案框选 |

---

## 📝 8. 注意事项

- 推荐使用 `XeLaTeX` 编译两次以确保题号、页码正确
- 如需修改字体，请在 `.cls` 文件中调整对应系统的字体名称
- 答案环境必须成对出现：`\\begin{answer}...\\end{answer}`
- 题目应放在 `\\generateProblemTable` 之前定义

---

## 📁 9. 目录结构建议

```
your-folder/
├── exam-cau.cls       ← 本模板类文件
└── main.tex           ← 用户主文档

```

---

## 🎉 10. 结语

本模板专为高校教师、助教设计，具有高度可读性和灵活性，适合用于期中期末考试、模拟试题等场景。

---

## 注记

本模版是在多个 AI 大语言模型的帮助下设计完成的。

