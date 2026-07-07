# 1013R_R108 备课室壳层与上传教案解析交接文档

交接时间：2026-07-05  
工作目录：`D:\Documents\SmartEdu\xiaobei-core`  
当前主线：`1013R` 备课室 / 备课本壳层 / 上传教案只读解析预览  
当前状态：R108 已完成“R97B 工作壳导入弹窗接 MarkItDown 后端解析 route”的 smoke。  

## 1. 给下一会话的第一句话

当前不要再新开一张教师静态页，也不要把 R100 的旧上传预览页当壳层。

当前受控工作壳是：

```text
outputs/PREP_ROOM_RENDER_CANVAS_DEEPEN_V1/1013R_R97B_TEACHER_SHELL_EXPERIENCE_POLISH_AND_STALE_CONTENT_CLEANUP/r97b_clean_shell_context_preview.html
```

当前用户浏览器还可能停在旧页：

```text
outputs/PREP_ROOM_RENDER_CANVAS_DEEPEN_V1/1013R_R100_P1_UPLOADED_LESSON_SHELL_CONTEXT_CONSISTENCY_REPAIR/uploaded_lesson_clean_shell_preview.html
```

这个 R100-P1 页面不是当前真实壳层工作页。它只能作为旧上传教案上下文一致性预览，不应继续作为壳层接入目标。

## 2. 当前项目结构速览

仓库根目录：

```text
D:\Documents\SmartEdu\xiaobei-core
```

关键顶层目录：

```text
backend/          后端 Python 模块，主要业务 API 和只读 preview route 在 backend/xiaobei_ai
frontend/         较早的前端页面与工作台 HTML
scripts/          本地 smoke、构建、验证、启动脚本
outputs/          1013R 等阶段产物、静态壳层、review package、validator
docs/             合同、报告、handoff、audit 文档
knowledge-base/   教材、教案、知识库资料；当前 docx 样本来自 lesson-cases
fixtures/         fixture / process stream 等测试数据
business_packs/   业务包
subject_packs/    学科包
data/             本地数据
memory/           项目内旧 memory 资料，不等同于 Codex 记忆
```

1013R 当前最重要输出目录：

```text
outputs/PREP_ROOM_RENDER_CANVAS_DEEPEN_V1/
```

这条线里页面很多，不能凭名字随便接。当前壳层路线大致是：

```text
R91A  原 R39 产品候选壳层静态回填
R97A  P6 教师课堂导航版接入壳层预览
R97A2 教学过程槽位绑定修复
R97A3 壳层上下文与右栏材料对齐
R97B  教师壳层体验修正、旧内容清理，当前工作壳
R100  上传教案 ingestion sandbox
R100-P1 上传教案 clean shell preview，旧页，不是当前工作壳
R101/R101-P1 多上传样本回归、字段分类修复
R101A/R101B 真实备课室只读壳层 fixture 回归
R103  真实上传入口 preview 后端 ViewModel route
R104A 备份机制和版本索引
R104B-R104E 导入按钮、粘贴/txt/md 解析、micro-step 支架预填
R105A/R105B 将导入能力受控应用到 R97B 工作壳，并清理教师可见工程词
R106  在同一 R97B 工作壳启用粘贴/txt/md 只读 smoke
R107A MarkItDown 后端文档抽取 route
R108  将 R97B 导入弹窗接到 MarkItDown 后端 route
```

## 3. 用户的核心约束和偏好

请严格遵守：

```text
1. 不要丢壳层。
2. 尽量不要新开静态页。
3. 如果必须开新静态页，必须先用大字告诉用户审核。
4. 不能把字段实验室或旧预览页误当教师端壳层。
5. 教师默认视图不能暴露工程字段、canonical、R88-GEN、lineage 等。
6. 教师第一眼要看到课堂怎么走、当前能做什么、哪里需确认。
7. micro-step、大屏、支架、小教、证据可以折叠，默认不要铺满。
8. 所有上传解析目前都是 preview only，不保存、不写库、不 formal apply。
9. 做坏要能回滚，所以每次改 R97B 工作壳前都要备份。
```

用户最关心的体验判断：

```text
字段越硬，前台越不能直接暴露字段。
教师端应是任务视角、成果视角、审核视角。
证据链必须有，但默认藏起来。
```

## 4. 当前壳层身份：谁是壳，谁不是

### 当前受控工作壳

```text
outputs/PREP_ROOM_RENDER_CANVAS_DEEPEN_V1/1013R_R97B_TEACHER_SHELL_EXPERIENCE_POLISH_AND_STALE_CONTENT_CLEANUP/r97b_clean_shell_context_preview.html
```

这是当前应该继续接入的工作壳。R105A、R105B、R106、R108 都是在这个文件上推进。

### 原 R39/R91A 壳层候选

```text
outputs/PREP_ROOM_RENDER_CANVAS_DEEPEN_V1/1013R_R91A_STATIC_PAGE_BACKFILL/R91A_static_page_backfill_from_R39_product_candidate_preview.html
```

用户明确说过这个才是壳层源头之一。后续如果怀疑壳层结构丢失，应回看 R91A 和 R97A2/R97B，而不是直接拿 R100 页面改。

### 旧上传预览页，不再作为壳层

```text
outputs/PREP_ROOM_RENDER_CANVAS_DEEPEN_V1/1013R_R100_P1_UPLOADED_LESSON_SHELL_CONTEXT_CONSISTENCY_REPAIR/uploaded_lesson_clean_shell_preview.html
```

这个页面用于 R100-P1 上传教案上下文一致性修复。当用户浏览器还开着它时，不代表它是当前壳层。

### 被归档/不要再用的误接方向

之前有过把生成内容接进“独立教师页/字段页/旧上传页”的风险。下一会话必须先问：

```text
我要改的是 R97B 工作壳，还是只是做一个临时质量预览？
```

如果是教师可用壳层接入，默认目标必须是 R97B 工作壳。

## 5. 当前 R108 做了什么

### 目标

把 R97B 工作壳的“导入已有教案”弹窗接到 MarkItDown 后端文档解析 route。

用户问题是：

```text
怎么还不能解析？
```

定位结果：

```text
MarkItDown 后端 route 已存在，但 file:// R97B 壳层弹窗仍是旧静态逻辑，只显示 docx/pdf 等待后续解析接口。
```

R108 已修复：

```text
1. R97B 弹窗文案改为 Word/PDF 调用本地 MarkItDown 解析服务。
2. 选择 .docx / .pdf 后，前端将 File 存为 backend_document_file_pending。
3. 点击“生成字段预览”时，前端 POST 到：
   /api/prep-room/uploaded-lesson-document-preview
4. 后端返回 ViewModel 后，回填到现有 R97B 壳层槽位：
   - 课题 / 单元
   - 一、本课依据
   - 二、学情分析
   - 三、教学目标
   - 四、教学重难点
   - 五、教学准备
   - 六、教学过程
   - 七、学习单与评价
   - 右侧环节栏
   - 底部小教上下文
5. 仍然 preview only，不保存、不写库、不覆盖原文。
```

### R108 输出包

```text
outputs/PREP_ROOM_RENDER_CANVAS_DEEPEN_V1/1013R_R108_WIRE_R97B_IMPORT_MODAL_TO_MARKITDOWN_BACKEND_ROUTE/
```

里面有：

```text
README.md
validate_1013R_R108_wire_r97b_import_modal_to_markitdown_backend_route_result.json
pre_r108_backup__r97b_clean_shell_context_preview.html
local_backend_8082.out.log
local_backend_8082.err.log
```

### R108 当前 validator 结论

```text
status = PASS_WITH_NOTES
frontend_modal_wired_to_backend_route = true
renders_backend_viewmodel_into_existing_shell_slots = true
http_multipart_route_smoke = PASS
sample = kb_art_g3_lesson_case_1_fd1b5bdf60_课时1_渐变的魅力_教案.docx
lesson_title = 渐变的魅力
episode_count = 6
formal_apply = false
database_written = false
R21_modified = false
R36_modified = false
R95_executed = false
```

## 6. 后端相关文件

### R103 上传入口 ViewModel route

```text
backend/xiaobei_ai/prep_room_real_upload_entry_preview_1013R_R103.py
```

关键 route：

```text
POST /api/prep-room/uploaded-lesson-entry-preview
POST /api/prep-room/uploaded-lesson-document-preview
POST /api/prep-room/uploaded-lesson-entry-preview/action
```

当前重要函数：

```text
handle_upload_document_preview(file_storage)
build_upload_session(raw_text, file_name)
build_readonly_viewmodel_from_upload_session(session)
normalize_episodes(raw_text)
parse_plain_process_episodes(raw_text)
section_between_any(raw_text, headings)
```

说明：

```text
R103 负责把抽出的文本转为只读 ViewModel。
R107A 只负责文档抽正文。
R108 前端负责把 R97B 弹窗接到 route 并渲染返回的 ViewModel。
```

### R107A 文档抽取器

```text
backend/xiaobei_ai/prep_room_document_text_extractor_1013R_R107A.py
```

用途：

```text
使用 Microsoft MarkItDown 抽取 docx/pdf/txt/md 正文。
```

当前限制：

```text
.docx：已可解析；部分样本可拆 6-7 个 episode，部分样本因源结构不同只抽出标题或少量环节。
.pdf：route 已接；文本层 PDF 可尝试；扫描版或乱码中文 PDF 需要 OCR/模型兜底。
.doc：旧 Word 格式当前不作为正文解析主路径。
```

重要：当前 `handle_upload_document_preview` 调用抽取器时：

```text
enable_model_ocr = false
```

也就是说 PDF OCR/模型识别还没真正启用。

### routes 注册

```text
backend/xiaobei_ai/routes.py
```

它已注册：

```text
prep_room_real_upload_entry_preview_1013R_R103.register_routes(bp, _cors_preflight)
```

注意 CORS 里允许 `Origin: null`，所以 `file://` 页面理论上可以请求本地 8082/18082 服务。

## 7. 本地测试服务

当前用于 file:// 壳层测试的本地服务脚本：

```text
scripts/start_workbench_ai_v13_local.py
scripts/start_workbench_ai_v13_local.ps1
```

R108 修改了 `scripts/start_workbench_ai_v13_local.py`：

```text
1. 增加 multipart/form-data 里 file 字段的简易解析。
2. 将 POST /api/prep-room/uploaded-lesson-document-preview 转发给 R103 的 handle_upload_document_preview。
3. 仍是本地只读服务，不写库、不保存、不导出。
```

启动命令：

```powershell
python scripts/start_workbench_ai_v13_local.py
```

或：

```powershell
powershell -ExecutionPolicy Bypass -File scripts/start_workbench_ai_v13_local.ps1
```

当前会监听：

```text
http://127.0.0.1:8082
```

当前会被 R97B file 页面尝试调用的候选后端：

```text
http://127.0.0.1:18082/api/prep-room/uploaded-lesson-document-preview
http://127.0.0.1:8082/api/prep-room/uploaded-lesson-document-preview
http://127.0.0.1:5177/api/prep-room/uploaded-lesson-document-preview
```

R108 当时已启动过 8082，本地进程是：

```text
python scripts/start_workbench_ai_v13_local.py
```

但是转会话后不要假定它还活着。先测：

```powershell
Invoke-WebRequest -UseBasicParsing -Uri "http://127.0.0.1:8082/api/workbench/ai/status" -TimeoutSec 5
```

## 8. 手工测试步骤

### 正确打开页面

打开：

```text
file:///D:/Documents/SmartEdu/xiaobei-core/outputs/PREP_ROOM_RENDER_CANVAS_DEEPEN_V1/1013R_R97B_TEACHER_SHELL_EXPERIENCE_POLISH_AND_STALE_CONTENT_CLEANUP/r97b_clean_shell_context_preview.html
```

不要打开：

```text
file:///D:/Documents/SmartEdu/xiaobei-core/outputs/PREP_ROOM_RENDER_CANVAS_DEEPEN_V1/1013R_R100_P1_UPLOADED_LESSON_SHELL_CONTEXT_CONSISTENCY_REPAIR/uploaded_lesson_clean_shell_preview.html
```

### 先确保后端在跑

```powershell
python scripts/start_workbench_ai_v13_local.py
```

如果 8082 已被占用，先查：

```powershell
Get-Process | Where-Object { $_.ProcessName -eq 'python' } | Select-Object Id,ProcessName,Path,StartTime
```

### 页面测试

1. 打开 R97B 工作壳。
2. 点击标题右上区域的“导入教案”按钮。
3. 上传 `.docx`。
4. 弹窗应显示“已选择：xxx.docx（点击生成字段预览后解析）”。
5. 点击“生成字段预览”。
6. 成功后应回填中间备课本：
   - 课题变成上传文档的课题
   - 本课依据/学情/目标/重难点/准备更新
   - 六、教学过程出现上传文档拆出的 U01/U02...
   - 右侧栏显示上传文档环节
   - 底部小教上下文跟随上传文档
7. 当前不保存、不写库、不覆盖原文。

### 后端 HTTP smoke 命令

R108 已跑过类似 smoke：

```powershell
python - <<'PY'
from pathlib import Path
import json, urllib.request
sample = next(p for p in Path('knowledge-base/lesson-cases').glob('*.docx') if 'fd1b5bdf60' in p.name)
boundary='----xiaobei-r108-http-smoke'
body=(f'--{boundary}\r\nContent-Disposition: form-data; name="file"; filename="{sample.name}"\r\nContent-Type: application/vnd.openxmlformats-officedocument.wordprocessingml.document\r\n\r\n').encode('utf-8') + sample.read_bytes() + f'\r\n--{boundary}--\r\n'.encode('utf-8')
req=urllib.request.Request('http://127.0.0.1:8082/api/prep-room/uploaded-lesson-document-preview', data=body, headers={'Content-Type': f'multipart/form-data; boundary={boundary}'}, method='POST')
with urllib.request.urlopen(req, timeout=30) as resp: payload=json.loads(resp.read().decode('utf-8'))
current=payload.get('prep_view_patch',{}).get('current_lesson',{})
print(resp.status, payload.get('ok'), current.get('lesson_title'), len(current.get('process_steps',[])))
PY
```

预期：

```text
200 True 渐变的魅力 6
```

## 9. 关键备份和回滚

总索引：

```text
outputs/PREP_ROOM_RENDER_CANVAS_DEEPEN_V1/1013R_R104A_SHELL_BASELINE_BACKUP_BEFORE_IMPORT_BUTTON/SHELL_VERSION_INDEX.md
```

R108 备份：

```text
outputs/PREP_ROOM_RENDER_CANVAS_DEEPEN_V1/1013R_R108_WIRE_R97B_IMPORT_MODAL_TO_MARKITDOWN_BACKEND_ROUTE/pre_r108_backup__r97b_clean_shell_context_preview.html
```

如果 R108 前端改坏，回滚方式：

```powershell
Copy-Item -LiteralPath "outputs/PREP_ROOM_RENDER_CANVAS_DEEPEN_V1/1013R_R108_WIRE_R97B_IMPORT_MODAL_TO_MARKITDOWN_BACKEND_ROUTE/pre_r108_backup__r97b_clean_shell_context_preview.html" -Destination "outputs/PREP_ROOM_RENDER_CANVAS_DEEPEN_V1/1013R_R97B_TEACHER_SHELL_EXPERIENCE_POLISH_AND_STALE_CONTENT_CLEANUP/r97b_clean_shell_context_preview.html" -Force
```

如果后端服务改坏，主要检查：

```text
scripts/start_workbench_ai_v13_local.py
backend/xiaobei_ai/prep_room_real_upload_entry_preview_1013R_R103.py
backend/xiaobei_ai/prep_room_document_text_extractor_1013R_R107A.py
```

## 10. Git / 工作区状态提醒

该仓库工作区非常脏，有大量历史未跟踪文件和旧修改。不要随便 reset，不要 checkout，不要清理未知文件。

本轮 R108 相关改动主要涉及：

```text
outputs/PREP_ROOM_RENDER_CANVAS_DEEPEN_V1/1013R_R97B_TEACHER_SHELL_EXPERIENCE_POLISH_AND_STALE_CONTENT_CLEANUP/r97b_clean_shell_context_preview.html
outputs/PREP_ROOM_RENDER_CANVAS_DEEPEN_V1/1013R_R108_WIRE_R97B_IMPORT_MODAL_TO_MARKITDOWN_BACKEND_ROUTE/
outputs/PREP_ROOM_RENDER_CANVAS_DEEPEN_V1/1013R_R104A_SHELL_BASELINE_BACKUP_BEFORE_IMPORT_BUTTON/SHELL_VERSION_INDEX.md
scripts/start_workbench_ai_v13_local.py
backend/xiaobei_ai/prep_room_real_upload_entry_preview_1013R_R103.py
backend/xiaobei_ai/prep_room_document_text_extractor_1013R_R107A.py
```

其中 `R103.py` 和 `R107A.py` 在 R107A/R108 前后已承担文档抽取与 ViewModel 构建。

## 11. 目前能做什么，不能做什么

### 已能做

```text
粘贴文本生成只读字段预览
txt/md 文件本地读取并生成只读字段预览
docx 文件经本地后端 MarkItDown 抽取后生成只读字段预览
部分 docx 可拆出 6-7 个教学环节
回填当前 R97B 壳层，不再生成新教师页
```

### 暂不能稳定做

```text
扫描版 PDF OCR
乱码中文 PDF 自动修复
旧 .doc 正文解析
所有 docx 都稳定拆出高质量 episode
保存到正式备课本
正式导出 PPT/PDF/DOCX
formal apply
写数据库/飞书/记忆
```

## 12. 下一步建议

建议下一轮先不要继续做新页面，按以下顺序：

```text
R109_IMPORT_DOCUMENT_PARSE_QUALITY_PATCH
```

目标：

```text
1. 用 5-10 个真实 docx 样本回归。
2. 统计每个样本：
   - 能否抽正文
   - 能否识别标题/年级/单元/目标/准备/评价
   - 能拆出几个 episode
   - 哪些字段是 uploaded_evidence
   - 哪些字段是 provisional_generated_candidate
3. 对 episode 为 0 或 1 的样本做解析规则修补。
4. 不改壳层结构，只提升解析质量。
```

之后再做：

```text
R110_PDF_OCR_OR_MODEL_FALLBACK_GATE
```

目标：

```text
明确 PDF 的三种状态：
1. 文本层 PDF，可 MarkItDown 直接抽取
2. 中文乱码 PDF，需要 OCR/模型
3. 扫描版 PDF，需要 OCR/模型
```

如果使用模型，必须新增成本/权限提示，不要静默调用。

## 13. 给下一会话 Codex 的强制执行规则

开始接手时先读：

```text
docs/handoff/1013R_R108_prep_room_import_shell_handoff_20260705.md
outputs/PREP_ROOM_RENDER_CANVAS_DEEPEN_V1/1013R_R104A_SHELL_BASELINE_BACKUP_BEFORE_IMPORT_BUTTON/SHELL_VERSION_INDEX.md
outputs/PREP_ROOM_RENDER_CANVAS_DEEPEN_V1/1013R_R108_WIRE_R97B_IMPORT_MODAL_TO_MARKITDOWN_BACKEND_ROUTE/README.md
outputs/PREP_ROOM_RENDER_CANVAS_DEEPEN_V1/1013R_R108_WIRE_R97B_IMPORT_MODAL_TO_MARKITDOWN_BACKEND_ROUTE/validate_1013R_R108_wire_r97b_import_modal_to_markitdown_backend_route_result.json
```

然后确认：

```text
1. 用户当前浏览器打开的是不是 R97B 工作壳。
2. 8082 本地只读服务是否运行。
3. /api/prep-room/uploaded-lesson-document-preview 是否能返回 200。
4. 不要再把 R100-P1 页面当壳层。
5. 不要新建教师静态页，除非用户明确授权。
```

如果用户问“为什么还不能解析”，优先排查：

```text
1. 当前打开的是 R97B 还是 R100 旧页。
2. 8082 服务是否启动。
3. 浏览器 file:// 是否能请求 127.0.0.1:8082。
4. 上传文件是 docx、pdf、txt/md，还是旧 doc。
5. PDF 是否是扫描版或乱码文本层。
```

## 14. 当前交接结论

```text
R108 = PASS_WITH_NOTES
壳层目标 = R97B working shell
Word/docx 解析 = 已通过 HTTP smoke
PDF = route 已接，OCR/乱码处理后置
保存/导出/正式应用 = 未开放
下一步 = R109 解析质量回归，不要先开新壳层页
```

