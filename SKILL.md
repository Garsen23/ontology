# Ontology Extractor Skill

## 1. 概述

本Skill旨在自动化从非结构化文档（PDF、Word、图片、PPT）中提取业务知识并进行本体建模的流程。它将非结构化输入转化为结构化数据，并结合本体建模方法论，辅助本体开发人员高效构建知识图谱。

## 2. 功能

*   **多格式文档处理**：支持PDF、Word、图片、PPT等多种非结构化文档的文本和图像内容提取。
*   **结构化信息抽取**：利用大语言模型（LLM）进行命名实体识别（NER）、关系抽取（RE）、属性抽取（AE）和事件抽取（EE），将非结构化文本转化为结构化数据。
*   **本体概念识别与构建**：根据预设的本体建模方法论，辅助识别本体中的Class、Property，并构建知识图谱。
*   **业务知识形式化**：将业务规则、概念定义等形式化为可用于本体开发的表示形式（如SPARQL查询、SWRL规则）。

## 3. 使用方法

本Skill通过命令行接口（CLI）或API调用，接收非结构化文档作为输入，并输出结构化数据、本体草稿或本体开发指导建议。

### 3.1 命令行使用示例 (概念性)

```bash
python3 main.py --input_file /path/to/your/document.pdf --output_dir ./output
```

### 3.2 输入参数

| 参数名        | 类型     | 描述                                                               | 示例值                     |
| :------------ | :------- | :----------------------------------------------------------------- | :------------------------- |
| `--input_file` | `string` | 待处理的非结构化文档路径（支持PDF, DOCX, PPTX, JPG, PNG）。 | `/home/user/report.pdf`    |
| `--output_dir` | `string` | 结构化输出文件和本体草稿的保存目录。                             | `./output_ontology`        |
| `--methodology_config` | `string` | 本体建模方法论的配置文件路径（可选，用于定制LLM行为）。 | `./methodology.json`       |

### 3.3 输出

Skill执行完成后，会在`--output_dir`指定的目录下生成以下文件：

*   `extracted_entities.json`：抽取到的实体、关系和属性的JSON格式文件。
*   `ontology_draft.owl`：初步构建的OWL本体文件草稿。
*   `knowledge_graph.ttl`：生成的RDF知识图谱文件（Turtle格式）。
*   `business_rules.txt`：形式化的业务规则列表。
*   `development_guide.md`：本体开发指导文档。

## 4. 依赖

本Skill依赖以下Python库：

*   `PyPDF2` / `pdfminer.six` (PDF处理)
*   `python-docx` (Word处理)
*   `python-pptx` (PPT处理)
*   `Pillow` (图像处理)
*   `Tesseract` (OCR，需额外安装)
*   `openai` 或其他LLM客户端库
*   `rdflib` (RDF/OWL处理)
*   `pyshacl` (SHACL验证)

请确保在运行前安装所有依赖：

```bash
pip install -r requirements.txt
```

## 5. 架构概览

本Skill的内部架构遵循以下流程：

1.  **文档解析**：根据文件类型调用相应的解析器，提取文本和图像。
2.  **OCR处理**：对图像文件和扫描版PDF进行光学字符识别。
3.  **LLM信息抽取**：利用LLM进行NER、RE、AE，将文本转化为结构化三元组。
4.  **本体映射与构建**：将抽取到的三元组映射到本体概念，并构建知识图谱。
5.  **规则形式化**：识别业务规则并将其形式化。
6.  **结果输出**：生成本体文件、知识图谱、业务规则和开发指导文档。

## 6. 维护与扩展

*   **LLM模型切换**：通过修改配置文件，可轻松切换不同的大语言模型。
*   **解析器扩展**：可根据需要添加对其他文档格式的解析支持。
*   **方法论定制**：`--methodology_config`参数允许用户提供定制的本体建模方法论，以指导LLM的抽取和建模行为。
