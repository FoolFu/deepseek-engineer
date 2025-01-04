# DeepSeek 工程师 🐋

## 概述

该仓库包含一个强大的编码助手应用程序，集成了 DeepSeek API，用于处理用户对话并生成结构化的 JSON 响应。通过直观的命令行界面，它可以读取本地文件内容、创建新文件，并实时对现有文件应用差异编辑。

---

## 主要功能

### 1. DeepSeek 客户端配置
- 自动配置 API 客户端以使用 DeepSeek 服务，需要有效的 `DEEPSEEK_API_KEY`。
- 连接到环境变量中指定的 DeepSeek 端点，以流式传输类似 GPT 的补全结果。

### 2. 数据模型
- 利用 Pydantic 进行类型安全的文件操作处理，包括：
  - **FileToCreate** – 描述要创建或更新的文件。
  - **FileToEdit** – 描述现有文件中特定片段的替换。
  - **AssistantResponse** – 结构化聊天响应和潜在的文件操作。

### 3. 系统提示
- 一个全面的系统提示 (`system_PROMPT`) 引导对话，确保所有回复严格遵循 JSON 输出，并可选择创建或编辑文件。

### 4. 辅助函数
- **`read_local_file`**：读取目标文件系统路径，并将其内容作为字符串返回。
- **`create_file`**：使用提供的内容创建或覆盖文件。
- **`show_diff_table`**：以丰富的多行表格形式展示提议的文件更改。
- **`apply_diff_edit`**：对现有文件应用片段级别的修改。

### 5. "/add" 命令
- 用户可以输入 `/add path/to/file` 快速读取文件内容，并将其作为系统消息插入到对话中。
- 这使得助手可以引用文件内容进行进一步讨论、代码生成或差异提案。

### 6. 对话流程
- 维护一个 `conversation_history` 列表，用于跟踪用户和助手之间的消息。
- 通过 DeepSeek API 流式传输助手的回复，并将其解析为 JSON，以保留文本响应和文件修改指令。

### 7. 交互式会话
- 运行脚本（例如：`python3 main.py`）以在终端启动交互式循环。
- 输入您的请求或代码问题。输入 `/add path/to/file` 将文件内容添加到对话中。
- 当助手建议创建新文件或编辑现有文件时，您可以直接在本地环境中确认更改。
- 输入 `exit` 或 `quit` 结束会话。

---

## 快速开始

### 1. 准备环境
创建一个 `.env` 文件，并包含您的 DeepSeek API 密钥：
```env
DEEPSEEK_API_KEY=your_api_key_here
```

### 2. 安装依赖并运行 选择以下一种方法运行：
   ### 使用 pip
   ```bash
   pip install -r requirements.txt
   python3 main.py
   ```

   ### 使用 uv（更快的替代方案）
   ```bash
   uv venv

   uv run main.py
   ```

## 3. 开始使用
- 享受多行流式响应。
- 使用 `/add path/to/file` 读取文件内容。
- 在批准时进行精确的文件编辑。

> **注意**：这是一个由 Skirano 开发的实验性项目，用于测试新的 DeepSeek v3 API 功能。它是作为快速原型开发的，应相应使用。

