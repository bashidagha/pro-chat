---
nav: 组件
group: Chat
title: ProChat
order: 0
description: a Chat Solution
---

## Default

通过返回流式 Response 请求，实现会话消息的打字机输出效果。

<code src="./demos/request.tsx"></code>

<code src="./demos/default.tsx"></code>

## SSE 数据流处理

对于后台直接返回 Server Side Event 数据的情况需要前端自己封装 `ReadableStream`

一般来说直接采用三方方案，例如 Vercel 的 AI 库进行解析即可，详情见 [文档 - 什么是流式输出](../guide/sse)

<code src="./demos/sse.tsx"></code>

## 错误处理

<code src="./demos/error.tsx"></code>

## SSE 的特殊处理

如果你觉得在 Request 里面封装 Reader 不是很方便，要对每次的 Stream 流做处理，我们提供了一个 transformToChatMessage api 来帮你做这个事情

<code src="./demos/sse-trans.tsx"></code>

## 大数据渲染

<code src="./demos/bigData.tsx"></code>

## 非流式模式

非流式模式下，会话消息会一次性全部返回，适用于消息量较少的场景。如果消息量较大，可能用户体验较差。

<code src="./demos/no-stream.tsx"></code>

## 受控模式

使用 `chats` 和 `onChatsChange` 实现 chats 会话消息的受控

<code src="./demos/control.tsx"></code>

## 设定初始会话消息

使用 `initialChats` 设定初始会话消息。

<code src="./demos/initialChats.tsx"></code>

## 设定打招呼消息

通过 `helloMessage` 设定打招呼消息。

<code src="./demos/helloMessage.tsx"></code>

## 加载中

使用 loading 字段控制加载中状态。适用于第一次加载数据时使用。

<code src="./demos/loading.tsx"></code>

## 文档模式

类 OpenAI 的文档模式，使用 `doc` 字段控制文档模式。适用于需要展示文档的场景。

<code src="./demos/doc-mode.tsx"></code>

## 指定会话双方的头像、名称

ProChat 使用 `meta` 来表意会话双方的头像、名称等信息。设定助手的头像、名称使用 `assistantMeta`，设定用户的头像、名称使用 `userMeta`。 使用 `showTitle` 显示名称。

<code src="./demos/meta.tsx"></code>

## assistantMeta和userMeta支持自定义className

`assistantMeta` 和 `userMeta` 通过接受 `className` 来支持自定义类名。

<code src="./demos/customeClassName.tsx"></code>

## 自定义 Actions

<code src="./demos/actions.tsx"></code>

## 自定义 Item 的 Actions

你可以使用 ChatItemConfig 下的 actionsRender 参数来完成每一个 Item 的 Actions 配置

> 我们并不建议你去修改，如果不想要可以直接删除这块功能自己用 render 来写

<code src="./demos/actions-chat-item.tsx"></code>

## 自定义「回到底部」按钮

你可以通过 backToBottomConfig 参数对「回到底部」按钮进行不同程度的自定义

<code src="./demos/toBottomConfig.tsx"></code>

## 自定义输入区域

有些时候会觉得默认的输入区域不够好用，或是你有一些输入模块的自定义需求，可以使用 inputAreaRender 来进行自定义输入，如果不需要输入区域可以传入 `inputAreaRender={()=>null}`。

下面是一个支持图片上传的示范案例，试试上传文件并提交看看吧。

<code src="./demos/renderInputArea.tsx"></code>

## 侧边栏使用

将 `ProChat` 组件作为会话解决方案，使用 antd 的 FloatButton 和 Modal 可以完成优雅的侧边栏模式。

<code src="./demos/float-drawer.tsx"></code>

## 监听对话时机

你可以使用 onChatStart、onChatEnd、onChatGenerate 来监听当前生成内容的回掉

> 注意，如果你手动通过 ref 触发了多个请求，可能会导致这些时机混乱出现，所以触发逻辑得注意。

<code src="./demos/listener.tsx"></code>

## 编程式操作控制

### chatRef

在一些简单场景下，使用 `chatRef` 可以获取 `ProChatInstance` ，以在组件同级控制 ProChat 行为。

<code src="./demos/use-ref.tsx"></code>

### useProChat

针对一些复杂场景，可以搭配 `ProChatProvider` 和 `useProChat` hooks， 实现编程式消息发送、获取、删除等行为。

<code src="./demos/use-pro-chat.tsx"></code>

:::warning

useProChat hooks 必须在包裹 `ProChatProvider` 后方可使用。

:::

:::warning

所有 `initialChats` 等初始化 props 需要从 `ProChat` 移动至 `ProChatProvider`

:::

## 国际化

<code src="./demos/i18n.tsx"></code>

## 自定义回调

<code src="./demos/callbacks.tsx"></code>

## APIs

| 参数 | 说明 | 类型 | 默认值 |
| --- | --- | --- | --- |
| showTitle | 是否显示标题 | Boolean | - |
| style | 样式 | CSSProperties | - |
| className | 主类名 | string | - |
| chatRef | 聊天引用，用于操作数据 | ProChatChatReference | - |
| loading | 是否加载中 | boolean | - |
| initialChats | 初始聊天记录 | ChatPropsState\['chats'] | - |
| userMeta | 用户元数据 | MetaData | - |
| assistantMeta | 助手元数据 | MetaData | - |
| config | 语言模型角色设定 | ModelConfig | - |
| onScroll | 滚动事件的监听 | onScroll: (e: Event) => void | - |
| chats | 聊天记录 | ChatMessage[] | - |
| onChatsChange | 聊天记录变化回调函数， | (chats: ChatMessage[]) => void | chat |
| displayMode | 显示模式，默认是 chat | 'chat' \| 'docs' | - |
| helloMessage | 欢迎消息 | string\| ReactNode | - |
| request | 请求消息 | string \| ChatRequest | - |
| onResetMessage | 重置消息回调函数 | `() => Promise<void>` | - |
| itemShouldUpdate | 判断每个子项是否需要重新 render | `(prevProps: ChatListItemProps, nextProps: ChatListItemProps) => boolean` | - |
| genMessageId | 生成消息 id 的函数，如果你的项目需要持久化时才需要使用 | \`() => Promise<string>\`\` | nanoid |
| autocompleteRequest | 获取自动完成列表的请求函数 | \`(value: string) => Promise<{ value: string; label?: string; }\[]>\`\` | - |
| placeholder | 输入框占位符 | string | - |
| messageItemExtraRender | 信息框额外渲染函数 | `(message: ChatMessage, type: 'assistant' \| 'user') => React.ReactNode` | - |
| actions | 信息框顶部的操作列表 | `{ flexConfig?: FlexBasicProps, render?: (defaultDoms: JSX.Element[]) => JSX.Element[] }` | - |
| actions.flexConfig | 控制 input 顶部的操作区域的 flex 布局 | `FlexBasicProps` | - |
| actions.render | 控制 input 顶部的操作区域的操作按钮 | `(defaultDoms: JSX.Element[]) => JSX.Element[]` | - |
| chatItemRenderConfig | 聊天项渲染配置 | `ChatItemRenderConfig` | - |
| backToBottomConfig | 透传给「回到底部」组件的 api | `BackBottomProps` | - |
| onChatEnd | 对话结束时候的回调，提供对话结束的详细信息和类型 | `(id: string, type: SSEFinishType) => void` | - |
| onChatStart | 对话开始时候的回调，提供开始时所有消息数组 | `(messages: ChatMessage<Record<string, any>>[]) => void` | - |
| onChatGenerate | 对话生成时候的回调，提供生成的文本块内容 | `(chunkText: string) => void` | - |

## ProChatChatReference

| 属性 | 说明 | 类型 | 默认值 |
| --- | --- | --- | --- |
| getChats | 获取当前聊天列表对象 | () => ChatStore['chats'] | - |
| getChatMessages | 获取当前聊天消息列表 | () => ChatMessage[] | - |
| setMessageContent | 设置消息内容 | (id: string, content: string) => void | - |
| setMessageValue | 修改消息的某个属性 | (id: string, key: keyof ChatMessage<Record<string, any>>, value: any) => void | - |
| scrollToBottom | 滚动到底部 | () => void | - |
| resendMessage | 重新发送消息 | (messageId: string) => void | - |
| stopGenerateMessage | 停止生成消息 | () => void | - |
| sendMessage | 发送消息 | (content: string) => void | - |
| deleteMessage | 删除消息 | (messageId: string) => void | - |
| clearMessage | 清除消息 | () => void | - |

## chatItemRenderConfig

| 参数 | 说明 | 类型 | 默认值 |
| --- | --- | --- | --- |
| titleRender | 标题渲染函数 | WithFalse<(props: ChatItemProps, defaultDom: ReactNode) => ReactNode> | - |
| contentRender | 内容渲染函数 | WithFalse<(props: ChatItemProps, defaultDom: ReactNode) => ReactNode> | - |
| actionsRender | 操作渲染函数 | WithFalse<(props: ChatItemProps, defaultDom: ReactNode) => ReactNode> | - |
| avatarRender | 头像渲染函数 | WithFalse<(props: ChatItemProps, defaultDom: ReactNode) => ReactNode> | - |
| render | 自定义渲染函数 | WithFalse<(props: ChatItemProps, defaultDom: { avatar: ReactNode; title: ReactNode; messageContent: ReactNode; actions: ReactNode; itemDom: ReactNode; }) => ReactNode> | - |

## backToBottomConfig

| 参数 | 说明 | 类型 | 默认值 |
| --- | --- | --- | --- |
| className | 类名 | string | - |
| style | 额外添加的css内容 | CSSProperties | - |
| onClick | 点击按钮的回掉 | `React.MouseEventHandler<HTMLElement>` | - |
| text | 展示的内容 | string | `Back to bottom` |
| render | 自定义渲染的方法 | (defaultDom: React.ReactNode,scrollToBottom,BackBottomConfig: BackBottomProps) => React.ReactNode | - |
| alwaysShow | 是否一直显示按钮 | boolean | false |
