# Ontology Extractor

从非结构化文档（PDF、Word、图片、PPT）中自动提取业务知识并进行本体建模。将非结构化输入转化为结构化数据，辅助本体开发人员高效构建知识图谱。

## 功能特性

- **多格式文档处理**：支持 PDF、Word、PPT、图片等多种非结构化文档
- **结构化信息抽取**：利用 LLM 进行命名实体识别（NER）、关系抽取（RE）、属性抽取（AE）和事件抽取（EE）
- **本体概念识别与构建**：辅助识别 Class、Property，构建知识图谱
- **业务知识形式化**：将业务规则、概念定义形式化为 SPARQL 查询、SWRL 规则等

## 快速开始

### 环境要求

- Python 3.9+
- [Tesseract OCR](https://github.com/tesseract-ocr/tesseract)（可选，用于图片/扫描件识别）

### 安装

```bash
git clone https://github.com/YOUR_USERNAME/ontology-extractor.git
cd ontology-extractor
pip install -r requirements.txt
```

### 使用

```bash
python main.py --input_file /path/to/document.pdf --output_dir ./output
```

#### 参数说明

| 参数 | 类型 | 说明 | 示例 |
|------|------|------|------|
| `--input_file` | string | 待处理的文档路径（PDF, DOCX, PPTX, JPG, PNG） | `./report.pdf` |
| `--output_dir` | string | 输出目录 | `./output` |
| `--methodology_config` | string | 本体建模方法论配置文件（可选） | `./methodology.json` |

### 输出文件

运行后将在输出目录生成：

| 文件 | 说明 |
|------|------|
| `extracted_entities.json` | 实体、关系和属性 |
| `ontology_draft.owl` | OWL 本体草稿 |
| `knowledge_graph.ttl` | RDF 知识图谱（Turtle 格式） |
| `business_rules.txt` | 形式化业务规则 |
| `development_guide.md` | 本体开发指导文档 |

## 架构

```
文档输入 → 文档解析 → OCR处理 → LLM信息抽取 → 本体映射与构建 → 规则形式化 → 输出
```

1. **文档解析**：根据文件类型调用对应解析器，提取文本和图像
2. **OCR 处理**：对图像文件和扫描版 PDF 进行光学字符识别
3. **LLM 信息抽取**：利用 LLM 进行 NER、RE、AE，将文本转化为结构化三元组
4. **本体映射与构建**：将三元组映射到本体概念，构建知识图谱
5. **规则形式化**：将业务规则转化为 SPARQL/SWRL 表示

## 项目结构

```
ontology-extractor/
├── main.py                 # 主程序入口
├── requirements.txt        # Python 依赖
├── SKILL.md                # OpenClaw Skill 描述文件
├── methodology.example.json # 方法论配置示例
├── LICENSE                 # 开源许可证
└── README.md               # 本文件
```

## 作为 OpenClaw Skill 使用

本项目同时也是一个 [OpenClaw](https://github.com/AgentrDev/OpenClaw) Skill。将 `skill-ontology-extractor` 文件夹放入 OpenClaw 的 `skills/` 目录即可使用。

## 许可证

MIT License
