---
name: arco-comment
description: Comment 评论
---

# Comment 评论

```tsx
import { Comment, Avatar } from '@arco-design/web-react';

<Comment
  author="张三"
  avatar={<Avatar>张</Avatar>}
  content="这是一条评论"
  datetime="2 小时前"
  actions={[<span key="reply">回复</span>, <span key="like">点赞</span>]}
/>

// 嵌套评论
<Comment author="张三" avatar={<Avatar>张</Avatar>} content="第一层评论">
  <Comment author="李四" avatar={<Avatar>李</Avatar>} content="回复评论" />
</Comment>
```

## API

| 属性 | 类型 | 说明 |
|------|------|------|
| `author` | `ReactNode` | 作者名 |
| `avatar` | `ReactNode` | 头像 |
| `content` | `ReactNode` | 评论内容 |
| `datetime` | `ReactNode` | 时间 |
| `actions` | `ReactNode[]` | 操作列表 |
| `align` | `{ datetime, actions }` | 对齐方式 |
