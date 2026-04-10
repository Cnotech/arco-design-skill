---
name: arco-vue-timeline
description: "Arco Design Vue 时间轴 Timeline 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-timeline>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 时间轴 Timeline

来源组件：上游 `web-vue/components/timeline`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-timeline>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
基本使用




```vue
<template>
  <div :style="{ marginBottom: '40px' }">
    <a-typography-text :style="{ verticalAlign: 'middle', marginRight: '8px' }">
      Reverse
    </a-typography-text>
    <a-radio-group
      @change="onChange"
      style="{ marginBottom: '30px' }"
      :modelValue="isReverse"
    >
      <a-radio :value="false">No Reverse</a-radio>
      <a-radio :value="true">Reverse</a-radio>
    </a-radio-group>
  </div>
  <a-timeline :reverse="isReverse">
    <a-timeline-item label="2017-03-10">The first milestone</a-timeline-item>
    <a-timeline-item label="2018-05-12">The second milestone</a-timeline-item>
    <a-timeline-item label="2020-09-30">The third milestone</a-timeline-item>
  </a-timeline>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const isReverse = ref(false);

    const onChange = (bool) => {
      isReverse.value = bool;
    };

    return {
      isReverse,
      onChange
    }
  },
};
</script>
```

## 示例：自定义节点内容

### 说明
自定义节点内容




```vue
<template>
  <a-timeline>
    <a-timeline-item label="2017-03-10" dotColor="#00B42A">
      The first milestone
    </a-timeline-item>
    <a-timeline-item label="2018-05-22">The second milestone</a-timeline-item>
    <a-timeline-item label="2020-06-22" dotColor="#F53F3F">
      The third milestone
      <IconExclamationCircleFill
        :style="{ color: 'F53F3F', fontSize: '12px', marginLeft: '4px' }"
      />
    </a-timeline-item>
    <a-timeline-item label="2020-09-30" dotColor="#C9CDD4">
      The fourth milestone
    </a-timeline-item>
  </a-timeline>
</template>

<script>
import { IconExclamationCircleFill } from '@arco-design/web-vue/es/icon';

export default {
  components: { IconExclamationCircleFill },
};
</script>
```

## 示例：自定义节点

### 说明
可以通过属性 `dotColor`, `dotType` 设置节点的颜色以及节点类型。同时可通过 `dot` 直接传入 DOM 自定义节点样式。优先级高于 `dotColor` 和 `dotType`




```vue
<template>
  <div :style="{ display: 'flex' }">
    <a-timeline :style="{ marginRight: '40px' }">
      <a-timeline-item label="2020-04-12" dotColor="#00B42A">
        The first milestone
      </a-timeline-item>
      <a-timeline-item label="2020-05-17">
        The second milestone
      </a-timeline-item>
      <a-timeline-item label="2020-06-22">
        <template #dot>
          <IconClockCircle :style="{ fontSize: '12px', color: '#F53F3F' }" />
        </template>
        The third milestone
      </a-timeline-item>
      <a-timeline-item label="2020-06-22" dotColor="var(--color-fill-4)">
        The third milestone
      </a-timeline-item>
    </a-timeline>

    <a-timeline :style="{ marginRight: '40px' }">
      <a-timeline-item label="2020-04-12">
        <template #dot>
          <IconCheck
            :style="{
              fontSize: '12px',
              padding: '2px',
              boxSizing: 'border-box',
              borderRadius: '50%',
              backgroundColor: 'var(--color-primary-light-1)',
            }"
          />
        </template>
        The first milestone
      </a-timeline-item>
      <a-timeline-item label="2020-05-17">
        <template #dot>
          <IconCheck
            :style="{
              fontSize: '12px',
              padding: '2px',
              boxSizing: 'border-box',
              borderRadius: '50%',
              backgroundColor: 'var(--color-primary-light-1)',
            }"
          />
        </template>
      </a-timeline-item>
      <a-timeline-item label="2020-06-22">The third milestone</a-timeline-item>
      <a-timeline-item label="2020-06-22" dotColor="var(--color-fill-4)">
        The third milestone
      </a-timeline-item>
    </a-timeline>

    <a-timeline>
      <a-timeline-item label="2020-04-12">The first milestone</a-timeline-item>
      <a-timeline-item label="2020-05-17" dotColor="var(--color-fill-4)">
        The second milestone
      </a-timeline-item>
      <a-timeline-item label="2020-06-22" dotColor="var(--color-fill-4)">
        The third milestone
      </a-timeline-item>
    </a-timeline>
  </div>
</template>

<script>
import { IconCheck } from '@arco-design/web-vue/es/icon';

export default {
  components: { IconCheck },
};
</script>
```

## 示例：自定义轴线样式

### 说明
自定义轴线的示例。




```vue
<template>
  <a-timeline>
    <a-timeline-item label="2017-03-10" lineType="dashed">
      The first milestone
      <br />
      <a-typography-text
        type="secondary"
        :style="{ fontSize: '12px', marginTop: '4px' }"
      >
        This is a descriptive message
      </a-typography-text>
    </a-timeline-item>
    <a-timeline-item label="2018-05-12" lineType="dashed">
      The second milestone
      <br />
      <a-typography-text
        type="secondary"
        :style="{ fontSize: '12px', marginTop: '4px' }"
      >
        This is a descriptive message
      </a-typography-text>
    </a-timeline-item>
    <a-timeline-item label="2020-09-30" lineType="dashed">
      The third milestone
      <br />
      <a-typography-text
        type="secondary"
        :style="{ fontSize: '12px', marginTop: '4px' }"
      >
        This is a descriptive message
      </a-typography-text>
    </a-timeline-item>
  </a-timeline>
</template>
```

## 示例：幽灵节点

### 说明
当任务状态正在发生，还在记录过程中，可用幽灵节点来表示当前的时间节点，通过`slot#pending-dot`定制其轴点。




```vue

<template>
  <a-row align="center" :style="{ marginBottom: '24px' }">
    <a-checkbox
      :checked="!!pendingProps.direction"
      @change="(v) => onChange({ direction: v ? 'horizontal' : '' })"
    >
      horizontal &nbsp; &nbsp;
    </a-checkbox>
    <a-checkbox
      :checked="!!pendingProps.reverse"
      @change="(v) => onChange({ reverse: v })"
    >
      reverse &nbsp; &nbsp;
    </a-checkbox>
    <a-checkbox
      :checked="!!pendingProps.pending"
      @change="
        (v) => onChange({ pending: v ? 'This is a pending dot' : false })
      "
    >
      pending &nbsp; &nbsp;
    </a-checkbox>

    <a-checkbox
      :checked="!!pendingProps.hasPendingDot"
      @change="(v) => onChange({ hasPendingDot: v })"
    >
      custom pendingDot
    </a-checkbox>
  </a-row>
  <a-timeline v-bind="pendingProps">
    <template v-if="pendingProps.hasPendingDot" #dot>
      <IconFire :style="{ color: '#e70a0a' }" />
    </template>
    <a-timeline-item label="2017-03-10" dotColor="#52C419">
      The first milestone
    </a-timeline-item>
    <a-timeline-item label="2018-05-12" dotColor="#F5222D">
      The second milestone
    </a-timeline-item>
    <a-timeline-item label="2020-09-30">The third milestone</a-timeline-item>
  </a-timeline>
</template>

<script>
import { ref } from 'vue';
import { IconFire } from '@arco-design/web-vue/es/icon';

export default {
  components: {
    IconFire,
  },
  setup() {
    const pendingProps = ref({});

    const onChange = (newProps) => {
      pendingProps.value = {
        ...pendingProps.value,
        ...newProps,
      };
    };

    return {
      pendingProps,
      onChange
    }
  },
};
</script>
```

## 示例：时间轴展示类型

### 说明
设置 `mode=alternate`时将会交替展示内容。同时可以通过设置 `TimelineItem` 的 `positon`属性控制时间轴节点的位置.




```vue
<template>
  <a-row justify="space-between">
    <a-timeline mode="alternate" :style="{ flex: 1 }">
      <a-timeline-item label="2017-03-10">The first milestone</a-timeline-item>
      <a-timeline-item label="2018-05-12">The second milestone</a-timeline-item>
      <a-timeline-item label="2020-09-30" position="bottom">
        The third milestone
      </a-timeline-item>
    </a-timeline>
    <a-timeline mode="right" :style="{ flex: 1 }">
      <a-timeline-item label="2017-03-10">The first milestone</a-timeline-item>
      <a-timeline-item label="2018-05-12">The second milestone</a-timeline-item>
      <a-timeline-item label="2020-09-30" position="bottom">
        The third milestone
      </a-timeline-item>
    </a-timeline>
  </a-row>
</template>
```

## 示例：纵向时间轴

### 说明
竖直方向的时间轴。




```vue
<template>
  <div>
    <a-row align="center" :style="{ marginBottom: '24px' }">
      <a-typography-text>mode: &nbsp; &nbsp;</a-typography-text>
      <a-radio-group @change="onChange" :modelValue="mode">
        <a-radio value="left">left</a-radio>
        <a-radio value="right">right</a-radio>
        <a-radio value="alternate">alternate</a-radio>
      </a-radio-group>
    </a-row>
    <a-timeline :mode="mode" labelPosition="relative">
      <a-timeline-item label="2012-08">
        <a-row :style="{ display: 'inline-flex', alignItems: 'center' }">
          <img
            width="40"
            :style="{ marginRight: '16px', marginBottom: '12px' }"
            src="https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/b5d834b83708a269b4562924436eac48.png~tplv-uwbnlip3yd-png.png"
          />
          <div :style="{ marginBottom: '12px' }">
            Toutiao
            <div :style="{ fontSize: '12px', color: '#4E5969' }">
              Founded in 2012
            </div>
          </div>
        </a-row>
      </a-timeline-item>
      <a-timeline-item label="2017-05">
        <a-row :style="{ display: 'inline-flex', alignItems: 'center' }">
          <img
            width="40"
            :style="{ marginRight: '16px', marginBottom: '12px' }"
            src="https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/385ed540c359ec8a9b9ce2b5fe89b098.png~tplv-uwbnlip3yd-png.png"
          />
          <div :style="{ marginBottom: '12px' }">
            Xigua Video
            <div :style="{ fontSize: '12px', color: '#4E5969' }">
              Founded in 2017
            </div>
          </div>
        </a-row>
      </a-timeline-item>
      <a-timeline-item label="2018-07">
        <a-row :style="{ display: 'inline-flex', alignItems: 'center' }">
          <img
            width="40"
            :style="{ marginRight: '16px', marginBottom: '12px' }"
            src="https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/385ed540c359ec8a9b9ce2b5fe89b098.png~tplv-uwbnlip3yd-png.png"
          />
          <div :style="{ marginBottom: '12px' }">
            Pipidance
            <div :style="{ fontSize: '12px', color: '#4E5969' }">
              Founded in 2018
            </div>
          </div>
        </a-row>
      </a-timeline-item>
    </a-timeline>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const mode = ref('left');

    const onChange = (_mode) => {
      mode.value = _mode;
    };

    return {
      mode,
      onChange
    }
  },
};
</script>
```

## 示例：横向时间轴

### 说明
可以通过 `direction` 设置展示横向时间轴




```vue
<template>
  <div>
    <a-row align="center" :style="{ marginBottom: '24px' }">
      <a-typography-text>mode: &nbsp; &nbsp;</a-typography-text>
      <a-radio-group @change="onChange" :modelValue="mode">
        <a-radio value="top">top</a-radio>
        <a-radio value="bottom">bottom</a-radio>
        <a-radio value="alternate">alternate</a-radio>
      </a-radio-group>
    </a-row>
    <a-timeline direction="horizontal" pending :mode="mode">
      <a-timeline-item label="2012-08">
        <a-row :style="{ display: 'inline-flex', alignItems: 'center' }">
          <img
            width="40"
            :style="{ marginRight: '16px', marginBottom: '12px' }"
            src="https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/b5d834b83708a269b4562924436eac48.png~tplv-uwbnlip3yd-png.png"
          />
          <div :style="{ marginBottom: '12px' }">
            Toutiao
            <div :style="{ fontSize: '12px', color: '#4E5969' }">
              Founded in 2012
            </div>
          </div>
        </a-row>
      </a-timeline-item>
      <a-timeline-item label="2017-05">
        <a-row :style="{ display: 'inline-flex', alignItems: 'center' }">
          <img
            width="40"
            :style="{ marginRight: '16px', marginBottom: '12px' }"
            src="https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/385ed540c359ec8a9b9ce2b5fe89b098.png~tplv-uwbnlip3yd-png.png"
          />
          <div :style="{ marginBottom: '12px' }">
            Xigua Video
            <div :style="{ fontSize: '12px', color: '#4E5969' }">
              Founded in 2017
            </div>
          </div>
        </a-row>
      </a-timeline-item>
      <a-timeline-item label="2018-07">
        <a-row :style="{ display: 'inline-flex', alignItems: 'center' }">
          <img
            width="40"
            :style="{ marginRight: '16px', marginBottom: '12px' }"
            src="https://p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/385ed540c359ec8a9b9ce2b5fe89b098.png~tplv-uwbnlip3yd-png.png"
          />
          <div :style="{ marginBottom: '12px' }">
            Pipidance
            <div :style="{ fontSize: '12px', color: '#4E5969' }">
              Founded in 2018
            </div>
          </div>
        </a-row>
      </a-timeline-item>
    </a-timeline>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const mode = ref('top');

    const onChange = (_mode) => {
      mode.value = _mode;
    };

    return {
      mode,
      onChange
    }
  },
};
</script>
```

## 示例：标签文本位置

### 说明
通过 `labelPosition` 可以设置标签文本的位置。




```vue
<template>
  <div>
    <a-row align="center">
      <a-typography-text>labelPosition: &nbsp; &nbsp;</a-typography-text>
      <a-radio-group @change="onLabelPositionChange" :modelValue="pos">
        <a-radio value="same">same</a-radio>
        <a-radio value="relative">relative</a-radio>
      </a-radio-group>
    </a-row>
    <a-row align="center" :style="{ margin: '20px 0px 24px' }">
      <a-typography-text>mode: &nbsp; &nbsp;</a-typography-text>
      <a-radio-group @change="onModeChange" :modelValue="mode">
        <a-radio value="left">left</a-radio>
        <a-radio value="right">right</a-radio>
        <a-radio value="alternate">alternate</a-radio>
      </a-radio-group>
    </a-row>
    <a-timeline :mode="mode" :labelPosition="pos">
      <a-timeline-item label="2017-03-10" dotColor="#52C419">
        The first milestone
      </a-timeline-item>
      <a-timeline-item
        label="2018-05-12"
        dotColor="#F5222D"
        labelPosition="same"
      >
        The second milestone
      </a-timeline-item>
      <a-timeline-item label="2020-09-30" position="bottom">
        The third milestone
      </a-timeline-item>
    </a-timeline>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const mode = ref('left');
    const pos = ref('same');

    const onLabelPositionChange = (_pos) => {
      pos.value = _pos;
    };

    const onModeChange = (_mode) => {
      mode.value = _mode;
    };

    return {
      mode,
      pos,
      onLabelPositionChange,
      onModeChange
    }
  },
};
</script>
```

## 示例：自定义标签

### 说明
可以通过 `label` 插槽自定义标签




```vue
<template>
  <a-timeline>
    <a-timeline-item>
      Code Review
      <template #label>
        <a-tag>
          <template #icon>
            <icon-check-circle-fill />
          </template>
          Passed
        </a-tag>
      </template>
    </a-timeline-item>
  </a-timeline>
</template>
```

## API


### `<timeline>` 属性

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|reverse|是否倒序|`boolean`|`false`|
|direction|时间轴方向|`'horizontal' \| 'vertical'`|`'vertical'`|
|mode|时间轴的展示类型：时间轴在左侧，时间轴在右侧, 交替出现。|`'left' \| 'right' \| 'top' \| 'bottom' \| 'alternate'`|`'left'`|
|pending|是否展示幽灵节点，设置为 true 时候只展示幽灵节点。传入字符串时，会作为节点内容展示。|`boolean\|string`|`-`|
|label-position|设置标签文本的位置|`'relative' \| 'same'`|`'same'`|
### `<timeline>` 插槽

|插槽名|描述|参数|
|---|:---:|---|
|dot|幽灵节点|-|




### `<timeline-item>` 属性

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|dot-color|节点颜色|`string`|`-`|
|dot-type|节点类型：空心圆/实心圆|`'hollow' \| 'solid'`|`'solid'`|
|line-type|时间轴类型：实线/虚线/点状线|`'solid' \| 'dashed' \| 'dotted'`|`'solid'`|
|line-color|时间轴颜色|`string`|`-`|
|label|标签文本|`string`|`-`|
|position|Item 位置|`PositionType`|`-`|
### `<timeline-item>` 插槽

|插槽名|描述|参数|版本|
|---|:---:|---|:---|
|dot|自定义节点|-||
|label|自定义标签|-|2.50.0|
