# 备课室渲染位地图

```text
stage_id=1013R_R13_XIAOJIAO_TASK_STATE_CONTRACT_AND_RENDER_SURFACE_MAP
map_id=PREP_ROOM_RENDER_SURFACE_MAP_R0
current_space=备课室
current_object=2-1《色彩的渐变》
```

## 原则

备课室不是一篇教案长文，也不是一个 AI 聊天框。

它应该是一组课堂工作对象的渲染空间：

```text
当前对象
小教任务状态
备课本正文
教学过程
教师示范
课件脚本
大屏呈现
学习单
评价表
板书设计
材料清单
资料来源与证据
教师确认动作
底部小教输入
```

当前阶段只定义渲染位、数据入口和动作边界，不做完整功能。

## 渲染位总表

| slot_id | 人话名称 | 数据来源 | 当前状态 | 动作边界 |
| --- | --- | --- | --- | --- |
| `current_object_card` | 当前课题卡 | `task_object`, `prep_view_patch.current_lesson` | 已绑定 | 只读 |
| `xiaojiao_task_state` | 小教任务状态 | `xiaojiao_task_state_contract` | 合同就绪 | 只读 |
| `lesson_body` | 备课本正文 | `prep_view_patch.current_lesson.sections` | 已绑定 | 预览后确认 |
| `teaching_process` | 教学过程 | `prep_view_patch.current_lesson.process_steps` | 已绑定 | 预览后确认 |
| `teacher_demo` | 教师示范 | `process_steps`, `courseware_screen_patch` | 占位 | 预览后确认 |
| `courseware_script` | 课件脚本 | `courseware_screen_patch` | 预览已绑定 | 预览后确认 |
| `classroom_display_screen` | 大屏呈现 | `big_screen_short_text`, `courseware_screen_patch` | 预览已绑定 | 预览后确认 |
| `worksheet` | 学习单 | `sections.assessment` | 占位 | 预览后确认 |
| `assessment_rubric` | 评价表 | `sections.assessment` | 占位 | 缺维度时阻断 |
| `blackboard_design` | 板书设计 | `flow`, 教师输入 | 占位 | 预览后确认 |
| `materials_list` | 材料清单 | `sections.preparation`, `source_matrix` | 预览已绑定 | 预览后确认 |
| `source_evidence` | 资料来源与证据 | `source_matrix`, `source_policy_notes` | 合同就绪 | 只读 |
| `confirm_actions` | 教师确认动作 | `runtime_actions`, `preview_candidates`, `blocked_actions` | 合同就绪 | 必须经过确认门 |
| `bottom_composer` | 底部小教输入 | `task_state`, `suggested_teacher_prompts` | 提示就绪 | 意图预览，不直接写入 |

## 大屏与课件的区别

后续不能把大屏和课件混成一个字段。

```text
courseware_script=课件/PPT 的屏幕结构、标题、页面顺序和素材状态
classroom_display_screen=上课时学生实际看到的大屏文字、图像、白板和任务提示
```

当前 R10 中的 `courseware_screen_patch` 可以同时喂给两者，但 R14 以后应逐步拆成：

```text
courseware_blocks
display_screen_blocks
```

## 资料来源标签

每个渲染位都必须能标明来源类型：

```text
textbook_anchor=教材依据
teacher_input=教师输入
ai_draft=AI 草案
external_reference=外部参考
system_structure=系统结构
teacher_input_required=需要教师补充
mixed_reference=混合参考，必须显示来源
```

当前规则：

```text
教材依据可以锚定当前课题和页码。
教师输入可以作为课堂条件和任务要求。
AI 草案只能作为草稿或参考。
系统结构只负责渲染和门控，不等同于教学依据。
```

## 渲染状态

```text
bound=已有后端 ViewModel 字段绑定
bound_as_preview=已有预览字段绑定，尚未 formal apply
contract_ready=协议字段已定义，等待页面适配
placeholder=渲染位已定义，功能未做实
blocked=缺少材料或教师确认，不能推进
future_only=未来能力
```

## 动作门控

```text
view_only=只能查看
intent_preview_only=只能识别/预览意图
preview_then_confirm=可生成预览，但教师确认前不写入
gate_required=必须走教师确认门
blocked_until_teacher_dimension=缺少教师维度时阻断
future_only=未来能力，不在当前阶段执行
```

## 对后续底座的意义

后续渲染底座不应该直接理解“教案是什么”，而应该吃稳定的渲染对象：

```text
render_surface_map
render_blocks
task_state
confirm_actions
source_policy_notes
```

R13 只定义地图。

R18/R19 以后再开始让页面吃 `render_blocks` 和轻量渲染适配器。
