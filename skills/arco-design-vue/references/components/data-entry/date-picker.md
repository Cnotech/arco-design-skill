---
name: arco-vue-date-picker
description: "Arco Design Vue 日期选择器 DatePicker 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-date-picker>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 日期选择器 DatePicker

来源组件：上游 `web-vue/components/date-picker`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-date-picker>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
日期输入器的基础使用。




```vue
<template>
  <a-date-picker style="width: 200px;" />
</template>
```

## 示例：月份选择器

### 说明
月份输入器的基础使用。




```vue
<template>
  <a-month-picker style="width: 200px;" />
</template>
```

## 示例：年份选择器

### 说明
年份输入器的基础使用。




```vue
<template>
  <a-year-picker style="width: 200px;" />
</template>
```

## 示例：季度选择器

### 说明
季度选择器的使用。




```vue
<template>
  <a-quarter-picker style="width: 200px;" />
</template>
```

## 示例：周选择器

### 说明
周选择器提供了一种选择星期的简单方法。也可以指定一周的起始日。




```vue
<template>
  <a-week-picker style="width: 200px; margin: 0 24px 24px 0;" />
  <a-week-picker
    style="width: 200px; margin: 0 24px 24px 0;"
    day-start-of-week="1"
  />
</template>
```

## 示例：带时间的日期选择

### 说明
使用 `showTime` 可以使用带时间的日期选择。




```vue
<template>
  <a-date-picker
    style="width: 220px; margin: 0 24px 24px 0;"
    show-time
    :time-picker-props="{ defaultValue: '09:09:06' }"
    format="YYYY-MM-DD HH:mm:ss"
    @change="onChange"
    @select="onSelect"
    @ok="onOk"
  />
  <a-date-picker
    style="width: 220px; margin: 0 24px 24px 0;"
    show-time
    format="YYYY-MM-DD hh:mm"
    @change="onChange"
    @select="onSelect"
    @ok="onOk"
  />
  <a-range-picker
    style="width: 360px; margin: 0 24px 24px 0;"
    show-time
    :time-picker-props="{ defaultValue: ['00:00:00', '09:09:06'] }"
    format="YYYY-MM-DD HH:mm"
    @change="onChange"
    @select="onSelect"
    @ok="onOk"
  />
</template>
<script>
export default {
  setup() {
    function onSelect(dateString, date) {
      console.log('onSelect', dateString, date);
    }

    function onChange(dateString, date) {
      console.log('onChange: ', dateString, date);
    }

    function onOk(dateString, date) {
      console.log('onOk: ', dateString, date);
    }
    return {
      onSelect,
      onChange,
      onOk,
    };
  }
}
</script>
```

## 示例：范围选择器

### 说明
范围输入器的基础使用。




```vue
<template>
  <a-range-picker
    @change="onChange"
    @select="onSelect"
    style="width: 254px; marginBottom: 20px;"
  />
  <br />
  <a-range-picker
    mode="week"
    @change="onChange"
    @select="onSelect"
    style="width: 254px; marginBottom: 20px;"
  />
  <br />
  <a-range-picker
    mode="month"
    @change="onChange"
    @select="onSelect"
    style="width: 254px; marginBottom: 20px;"
  />
  <br />
  <a-range-picker
    mode="year"
    @change="onChange"
    @select="onSelect"
    style="width: 254px; marginBottom: 20px;"
  />
  <br />
  <a-range-picker
    mode="quarter"
    @change="onChange"
    @select="onSelect"
    style="width: 254px; marginBottom: 20px;"
  />
  <br />
  <a-range-picker
    showTime
    :time-picker-props="{
    defaultValue:['00:00:00','00:00:00']
    }"
    @change="onChange"
    @select="onSelect"
    style=" width: 380px; "
  />
</template>
<script>
export default {
  setup() {
    return {
      onSelect(dateString, date) {
        console.log('onSelect', dateString, date);
      },
      onChange(dateString, date) {
        console.log('onChange: ', dateString, date);
      },
    };
  },
}
</script>
```

## 示例：默认值

### 说明
日期输入器有默认值的情况。




```vue
<template>
  <a-date-picker
    defaultValue="2019-06-03"
    @select="onSelect"
    @change="onChange"
    :style="style"
  />
  <a-date-picker
    defaultValue="2019-06-03"
    :format="(value) => `custom format: ${dayjs(value).format('YYYY-MM-DD')}`"
    @select="onSelect"
    @change="onChange"
    :style="{ ...style, width: '240px' }"
  />
  <a-date-picker
    showTime
    defaultValue="2019-06-03 08:00:00"
    @select="onSelect"
    @change="onChange"
    :style="style"
  />
  <a-year-picker
    defaultValue="2019"
    @select="onSelect"
    @change="onChange"
    :style="style"
  />
  <a-month-picker
    defaultValue="2019-06"
    @select="onSelect"
    @change="onChange"
    :style="style"
  />
  <a-week-picker
    :defaultValue="dayjs('2019-08-02')"
    @select="onSelect"
    @change="onChange"
    :style="style"
  />
  <a-range-picker
    showTime
    :defaultValue="['2019-08-08 00:00:00', '2019-08-18 00:00:00']"
    @select="onSelect"
    @change="onChange"
    :style="{ ...style, width: '360px' }"
  />
  <a-range-picker
    mode="month"
    :defaultValue="['2019-08', '2020-06']"
    @select="onSelect"
    @change="onChange"
    style="width: 300px; marginBottom: 24px;"
  />
</template>
<script>
import dayjs from 'dayjs';

export default {
  setup() {
    return {
      dayjs,
      onSelect(dateString, date) {
        console.log('onSelect', dateString, date);
      },
      onChange(dateString, date) {
        console.log('onChange: ', dateString, date);
      },
      style: { width: '200px', marginBottom: '24px', marginRight: '24px' }
    }
  }
}
</script>
```

## 示例：不可选取的时间

### 说明
使用 `disabledDate` 可以禁用某些日期。使用 `disabledTime` 可以禁用时间，需要配合 `showTime` 使用。




```vue
<template>
  <div>
    <a-date-picker
      style="width: 200px; margin-right: 24px; margin-bottom: 24px;"
      :disabledDate="(current) => dayjs(current).isBefore(dayjs())"
    />
    <a-range-picker
      style="width: 360px; margin-right: 24px; margin-bottom: 24px;"
      :disabledDate="(current) => dayjs(current).isBefore(dayjs())"
    />
    <a-date-picker
      style="width: 200px; margin-right: 24px; margin-bottom: 24px;"
      show-time
      :disabledDate="(current) => dayjs(current).isBefore(dayjs())"
      :disabledTime="getDisabledTime"
    />
    <a-range-picker
      style="width: 360px; margin-bottom: 24px;"
      show-time
      :timePickerProps="{hideDisabledOptions: true}"
      :disabledDate="(current) => dayjs(current).isBefore(dayjs())"
      :disabledTime="getDisabledRangeTime"
    />
  </div>
</template>
<script>
import dayjs from 'dayjs';

function range(start, end) {
  const result = [];
  for (let i = start; i < end; i++) {
    result.push(i);
  }
  return result;
}

function getDisabledTime(date) {
  return {
    disabledHours: () => range(6, 24),
    disabledMinutes: () => range(30, 60),
    disabledSeconds: () => range(30, 60),
  };
}

function getDisabledRangeTime(date, type) {
  return {
    disabledHours: () => type === 'start' ? range(0, 6): range(6, 24),
    disabledMinutes: () => type === 'end' ? range(0, 30) : [31, 60],
    disabledSeconds: () => range(30, 60),
  };
}

export default {
  setup() {
    return {
      dayjs,
      getDisabledTime,
      getDisabledRangeTime,
    }
  }
}
</script>
```

## 示例：预设时间快捷选择

### 说明
使用 `shortcuts` 可以预设时间快捷选择。




```vue
<template>
  <a-date-picker
    style="width: 300px; margin-bottom: 24px; margin-right: 24px;"
    :shortcuts="[
      {
        label: '2 hours later',
        value: () => dayjs().add(2, 'hour')
      },
      {
        label: 'a week later',
        value: () => dayjs().add(1, 'week'),
      },
      {
        label: 'a month later',
        value: () => dayjs().add(1, 'month'),
      },
    ]"
    show-time
  />
  <a-month-picker
    style="width: 300px; margin-bottom: 24px; margin-right: 24px;"
    :shortcuts="[
      {
        label: 'last month',
        value: () => dayjs().subtract(1, 'month'),
      },
      {
        label: 'six months later',
        value: () => dayjs().add(6, 'month'),
      },
      {
        label: 'two years later',
        value: () => dayjs().add(2, 'year'),
      },
    ]"
  />
  <a-range-picker
    style="width: 400px; margin-bottom: 24px; margin-right: 24px;"
    :shortcuts="[
      {
        label: 'next 7 days',
        value: () => [dayjs(), dayjs().add(1, 'week')],
      },
      {
        label: 'next 30 days',
        value: () => [dayjs(), dayjs().add(1, 'month')],
      },
      {
        label: 'next 365 days',
        value: () => [dayjs(), dayjs().add(1, 'year')],
      },
    ]"
  />
  <a-range-picker
    mode="month"
    style="width: 300px; margin-bottom: 24px;"
    :shortcuts="[
      {
        label: 'next 6 months',
        value: () => [dayjs(), dayjs().add(6, 'month')],
      },
      {
        label: 'next 12 months',
        value: () => [dayjs(), dayjs().add(1, 'year')],
      },
      {
        label: 'next 10 years',
        value: () => [dayjs(), dayjs().add(10, 'year')],
      },
    ]"
  />
</template>
<script>
import dayjs from 'dayjs';
export default {
  setup() {
    return {
      dayjs
    }
  }
}
</script>
```

## 示例：定制预设范围位置

### 说明
使用 `shortcutsPosition` 可以将预设时间快捷选择放到左边、右边或者底部。




```vue
<template>
  <a-date-picker
    style="width: 254px; margin-bottom: 20px; margin-right: 24px;"
    shortcuts-position="left"
    :shortcuts="shortcuts"
  />
  <a-range-picker
    style="width: 300px; margin-bottom: 20px;"
    shortcuts-position="left"
    :shortcuts="rangeShortcuts"
  />
  <br />
  <a-date-picker
    style="width: 254px; margin-right: 24px;"
    shortcuts-position="right"
    :shortcuts="shortcuts"
  />
  <a-range-picker
    style="width: 300px;"
    shortcuts-position="right"
    :shortcuts="rangeShortcuts"
  />
</template>
<script>
import dayjs from 'dayjs';
export default {
  setup() {
    return {
      dayjs,
      shortcuts: [
        {
          label: 'yesterday',
          value: () => dayjs().subtract(1, 'day')
        },
        {
          label: 'today',
          value: () => dayjs(),
        },
        {
          label: 'a week later',
          value: () => dayjs().add(1, 'week'),
        },
        {
          label: 'a month later',
          value: () => dayjs().add(1, 'month'),
        },
        {
          label: '2 months later',
          value: () => dayjs().add(2, 'month'),
        }
      ],
      rangeShortcuts: [
        {
          label: 'next 2 days',
          value: () => [dayjs(), dayjs().add(2, 'day')],
        },
        {
          label: 'next 7 days',
          value: () => [dayjs(), dayjs().add(1, 'week')],
        },
        {
          label: 'next 30 days',
          value: () => [dayjs(), dayjs().add(1, 'month')],
        },
        {
          label: 'next 6 months',
          value: () => [dayjs(), dayjs().add(6, 'month')],
        },
        {
          label: 'next 12 months',
          value: () => [dayjs(), dayjs().add(1, 'year')],
        },
        {
          label: 'next 10 years',
          value: () => [dayjs(), dayjs().add(10, 'year')],
        }
      ]
    }
  }
}
</script>
```

## 示例：动态控制选取范围

### 说明
根据选择的值来控制选取的范围，使用 `onSelect` 配合 `disabledDate` 来实现。




```vue
<template>
  <a-range-picker
      style="width: 300px;"
      @select="onSelect"
      @popupVisibleChange="onPopupVisibleChange"
      :disabledDate="disabledDate"
    />
</template>
<script>
export default {
  data() {
    return {
      dates: [],
    }
  },
  methods: {
    onSelect(valueString, value) {
      this.dates = value;
    },
    onPopupVisibleChange(visible) {
      if (!visible) {
        this.dates = []
      }
    },
    disabledDate(current) {
      const dates = this.dates;
      if (dates && dates.length) {
        const tooLate = dates[0] && Math.abs((new Date(current) - dates[0]) / (24 * 60 * 60 * 1000)) > 7;
        const tooEarly = dates[1] && Math.abs((new Date(current) - dates[1]) / (24 * 60 * 60 * 1000)) > 7;
        return tooEarly || tooLate;
      }
      return false;
    }
  }
}
</script>
```

## 示例：尺寸

### 说明
设置 `size` 可以使用四种尺寸（`mini` `small` `medium` `large`）的输入框。高度分别对应 24px、28px、32px、36px。




```vue
<template>
  <div style="margin-bottom: 20px;">
    <a-radio-group v-model="size" type='button'>
      <a-radio value="mini">mini</a-radio>
      <a-radio value="small">small</a-radio>
      <a-radio value="medium">medium</a-radio>
      <a-radio value="large">large</a-radio>
    </a-radio-group>
  </div>
  <a-date-picker
    :size="size"
    style="width: 254px;"
  />
</template>
<script>
export default {
  data() {
    return {
      size: 'small'
    }
  }
}
</script>
```

## 示例：额外的页脚

### 说明
在浮层中加入额外的页脚，以满足某些定制信息的需求。




```vue
<template>
  <a-date-picker style="width: 200px; margin-bottom: 20px">
    <template #extra>Extra footer</template>
  </a-date-picker>
  <br />
  <a-range-picker showTime style="width: 360px;">
    <template #extra>Extra footer</template>
  </a-range-picker>
</template>
```

## 示例：禁用

### 说明
禁用状态。




```vue
<template>
  <a-date-picker
    defaultValue="2020-08-08"
    disabled
    style="width: 200px; margin-bottom: 20px;"
  />
  <br />
  <a-range-picker
    :defaultValue="['2020-08-08', '2020-08-18']"
    disabled
    style="width: 300px; margin-bottom: 20px;"
  />
  <br />
  <a-range-picker
    :defaultValue="['2020-08-08']"
    :disabled="[true, false]"
    :disabledDate="(current) => dayjs(current).isBefore(dayjs('2020-08-08'))"
    style="width: 300px; margin-bottom: 20px;"
  />
  <br />
  <a-range-picker
    showTime
    :defaultValue="['2020-08-08 02:02:02']"
    :disabled="[true, false]"
    style="width: 380px;"
  />
</template>
<script>
import dayjs from 'dayjs';
export default {
  setup() {
    return {
      dayjs
    };
  }
}
</script>
```

## 示例：定制日期单元格

### 说明
利用具名插槽  `cell` 可以定制日期单元格。




```vue
<template>
  <a-date-picker>
    <template #cell="{ date }">
      <div class="arco-picker-date">
        <div class="arco-picker-date-value" :style="getCellStyle(date)">
          {{ date.getDate() }}
        </div>
      </div>
    </template>
  </a-date-picker>
</template>
<script>
export default {
  setup() {
    const highlightDates = [6, 14, 22];
    const highlightStyle = {
      border: '1px solid rgb(var(--arcoblue-6))',
    };
    return {
      getCellStyle(date) {
        return highlightDates.includes(date.getDate()) ? highlightStyle : {}
      }
    }
  }
}
</script>
```

## 示例：双向绑定

### 说明
通过 `v-model` 实现值的双向绑定




```vue
<template>
  <a-space>
    <a-date-picker v-model="value" style="width: 200px;" />
    <a-range-picker v-model="rangeValue" style="width: 300px;" />
  </a-space>
</template>
<script>
export default {
  data() {
    return {
      value: Date.now(),
      rangeValue: [Date.now(), Date.now()],
    }
  }
}
</script>
```

## 示例：自定义触发元素

### 说明
自定义触发元素。




```vue
<template>
  <a-space>
    <a-date-picker
      style="width: 268px;"
      v-model="value"
    >
      <a-button>{{ value || '请选择日期' }}</a-button>
    </a-date-picker>
    <a-range-picker
      style="width: 268px;"
      v-model="rangeValue"
    >
      <a-button>{{ rangeValue && rangeValue.join(' - ') || '请选择日期范围' }}</a-button>
    </a-range-picker>
  </a-space>
</template>
<script>
import { ref } from 'vue';
export default {
  setup() {
    const value = ref();
    const rangeValue = ref();
    return {
      value,
      rangeValue,
    }
  }
}
</script>
```

## 示例：只使用面板

### 说明
只用选择面板，不显示输入框。




```vue
<template>
  <div>
    <a-date-picker
      default-value="2019-06-03"
      v-model:pickerValue="pickerValue"
      hide-trigger
      style="width: 268px;"
    />
    <a-range-picker
      :default-value="['2019-08-01', '2020-06-01']"
      v-model:pickerValue="rangePickerValue"
      hide-trigger
      style="width: 560px; margin-top: 20px;"
    />
  </div>
</template>
<script>
export default {
  data() {
    return {
      pickerValue: null,
      rangePickerValue: null,
    };
  }
};
</script>
```

## API


### `Common` Props

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|locale|国际化配置，用于覆盖locale中的 `datePicker` 字段|`Record<string, any>`|`-`||
|hide-trigger|没有触发元素，只显示选择面板|`boolean`|`false`||
|allow-clear|是否允许清除|`boolean`|`true`||
|readonly|是否为只读|`boolean`|`false`||
|error|是否为错误状态|`boolean`|`false`||
|size|日期选择器的尺寸|`'mini' \| 'small' \| 'medium' \| 'large'`|`'medium'`||
|shortcuts|预设时间范围快捷选择|`ShortcutType[]`|`[]`||
|shortcuts-position|预设范围在面板上的位置，默认放在下方，侧边一般用于大量预设时间的场景|`'left' \| 'bottom' \| 'right'`|`'bottom'`||
|position|弹出的框的位置|`'top' \| 'tl' \| 'tr' \| 'bottom' \| 'bl' \| 'br'`|`'bl'`||
|popup-visible|控制弹出框的打开或者关闭状态|`boolean`|`-`||
|default-popup-visible|默认弹出框是打开或者关闭|`boolean`|`false`||
|trigger-props|可以传入 `Trigger` 组件的参数|`TriggerProps`|`-`||
|unmount-on-close|是否在隐藏的时候销毁DOM结构|`boolean`|`false`||
|placeholder|提示文案|`string`|`-`||
|disabled|是否禁用|`boolean`|`false`||
|disabled-date|不可选取的日期|`(current?: Date) => boolean`|`-`||
|disabled-time|不可选取的时间|`(current: Date) => DisabledTimeProps`|`-`||
|picker-value **(v-model)**|面板显示的日期|`Date \| string \| number`|`-`||
|default-picker-value|面板默认显示的日期|`Date \| string \| number`|`-`||
|popup-container|弹出框的挂载容器|`string \| HTMLElement`|`-`||
|value-format|值的格式，对 `value` `defaultValue` `pickerValue` `defaultPickerValue` 以及事件中的返回值生效，支持设置为时间戳，Date 和字符串（参考[字符串解析格式](#字符串解析格式)）。如果没有指定，将格式化为字符串，格式同 `format`。|`'timestamp' \| 'Date' \| string`|`-`|2.16.0|
|preview-shortcut|是否要预览快捷选择的结果|`boolean`|`true`|2.28.0|
|show-confirm-btn|是否显示确认按钮，`showTime = true` 的时候始终显示。|`boolean`|`false`|2.29.0|
|disabled-input|是否禁止键盘输入日期|`boolean`|`false`|2.43.0|
|abbreviation|是否启用缩写|`boolean`|`true`|2.45.0|
### `Common` Events

|事件名|描述|参数|
|---|---|---|
|change|组件值发生改变|value: `Date \| string \| number \| undefined`<br>date: `Date \| undefined`<br>dateString: `string \| undefined`|
|select|选中日期发生改变但组件值未改变|value: `Date \| string \| number`<br>date: `Date`<br>dateString: `string`|
|popup-visible-change|打开或关闭弹出框|visible: `boolean`|
|ok|点击确认按钮|value: `Date \| string \| number`<br>date: `Date`<br>dateString: `string`|
|clear|点击清除按钮|-|
|select-shortcut|点击快捷选项|shortcut: `ShortcutType`|
|picker-value-change|面板日期改变|value: `Date \| string \| number`<br>date: `Date`<br>dateString: `string`|
### `Common` Slots

|插槽名|描述|参数|版本|
|---|:---:|---|:---|
|prefix|输入框前缀|-|2.41.0|
|suffix-icon|输入框后缀图标|-||
|icon-next-double|双箭头往后翻页图标|-||
|icon-prev-double|双箭头往前翻页图标|-||
|icon-next|单箭头往后翻页图标|-||
|icon-prev|单箭头往前翻页图标|-||
|cell|自定义日期单元格的内容|date: `Date`||
|extra|额外的页脚|-||




### `<date-picker>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|model-value **(v-model)**|绑定值|`Date \| string \| number`|`-`||
|default-value|默认值|`Date \| string \| number`|`-`||
|format|展示日期的格式，参考[字符串解析格式](#字符串解析格式)|`string \| ((current: Date) => string)`|`-`||
|day-start-of-week|每周的第一天开始于周几，0 - 周日，1 - 周一，以此类推。|`0 \| 1 \| 2 \| 3 \| 4 \| 5 \| 6`|`0`|2-6 from 2.21.0|
|show-time|是否增加时间选择|`boolean`|`false`||
|time-picker-props|时间显示的参数，参考 [TimePickerProps](/vue/component/time-picker)|`Partial<TimePickerProps>`|`-`||
|disabled|是否禁用|`boolean`|`false`||
|disabled-date|不可选取的日期|`(current?: Date) => boolean`|`-`||
|disabled-time|不可选取的时间|`(current: Date) => DisabledTimeProps`|`-`||
|show-now-btn|是否显示 `showTime` 时，选择当前时间的按钮|`boolean`|`true`||




### `<month-picker>` 属性

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|model-value **(v-model)**|绑定值|`Date \| string \| number`|`-`|
|default-value|默认值|`Date \| string \| number`|`-`|
|format|展示日期的格式，参考[字符串解析格式](#字符串解析格式)|`string`|`'YYYY-MM'`|




### `<year-picker>` 属性

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|model-value **(v-model)**|绑定值|`Date \| string \| number`|`-`|
|default-value|默认值|`Date \| string \| number`|`-`|
|format|展示日期的格式，参考[字符串解析格式](#字符串解析格式)|`string`|`'YYYY'`|




### `<quarter-picker>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|model-value **(v-model)**|绑定值|`Date \| string \| number`|`-`||
|default-value|默认值|`Date \| string \| number`|`-`||
|format|展示日期的格式，参考[字符串解析格式](#字符串解析格式)|`string`|`'YYYY-[Q]Q'`||
|value-format|值的格式，对 `value` `defaultValue` `pickerValue` `defaultPickerValue` 以及事件中的返回值生效，支持设置为时间戳，Date 和字符串（参考[字符串解析格式](#字符串解析格式)）。|`string`|`'YYYY-MM'`|2.16.0|




### `<week-picker>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|model-value **(v-model)**|绑定值|`Date \| string \| number`|`-`||
|default-value|默认值|`Date \| string \| number`|`-`||
|format|展示日期的格式，参考[字符串解析格式](#字符串解析格式)|`string`|`'gggg-wo'`||
|value-format|值的格式，对 `value` `defaultValue` `pickerValue` `defaultPickerValue` 以及事件中的返回值生效，支持设置为时间戳，Date 和字符串（参考[字符串解析格式](#字符串解析格式)）。|`string`|`'YYYY-MM-DD'`|2.16.0|
|day-start-of-week|每周的第一天开始于周几，0 - 周日，1 - 周一，以此类推。|`0 \| 1 \| 2 \| 3 \| 4 \| 5 \| 6`|`0`|2-6 from 2.21.0|




### `<range-picker>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|mode|范围选择器的类型|`'date' \| 'year' \| 'quarter' \| 'month' \| 'week'`|`'date'`||
|model-value **(v-model)**|绑定值|`(Date \| string \| number)[]`|`-`||
|default-value|默认值|`(Date \| string \| number)[]`|`-`||
|picker-value|默认面板显示的日期|`(Date \| string \| number)[]`|`-`||
|default-picker-value|面板显示的日期|`(Date \| string \| number)[]`|`-`||
|disabled|是否禁用|`boolean \| boolean[]`|`false`||
|day-start-of-week|每周的第一天开始于周几，0 - 周日，1 - 周一，以此类推。|`0 \| 1 \| 2 \| 3 \| 4 \| 5 \| 6`|`0`|2-6 from 2.21.0|
|format|展示日期的格式，参考[字符串解析格式](#字符串解析格式)|`string`|`-`||
|value-format|值的格式，对 `value` `defaultValue` `pickerValue` `defaultPickerValue` 以及事件中的返回值生效，支持设置为时间戳，Date 和字符串（参考[字符串解析格式](#字符串解析格式)）。如果没有指定，将格式化为字符串，格式同 `format`。|`'timestamp' \| 'Date' \| string`|`-`|2.16.0|
|show-time|是否增加时间选择|`boolean`|`false`||
|time-picker-props|时间显示的参数，参考 [TimePickerProps](/vue/component/time-picker)|`Partial<TimePickerProps>`|`-`||
|placeholder|提示文案|`string[]`|`-`||
|disabled-date|不可选的日期|`(current: Date, type: 'start' \| 'end') => boolean`|`-`||
|disabled-time|不可选取的时间|`(current: Date, type: 'start' \| 'end') => DisabledTimeProps`|`-`||
|separator|范围选择器输入框内的分割符号|`string`|`-`||
|exchange-time|时间是否会交换，默认情况下时间会影响和参与开始和结束值的排序，如果要固定时间顺序，可将其关闭。|`boolean`|`true`|2.25.0|
|disabled-input|是否禁止键盘输入日期|`boolean`|`false`|2.43.0|
|abbreviation|是否启用缩写|`boolean`|`true`||
### `<range-picker>` 事件

|事件名|描述|参数|
|---|---|---|
|change|组件值发生改变|value: `(Date \| string \| number \| undefined)[] \| undefined`<br>date: `(Date \| undefined)[] \| undefined`<br>dateString: `(string \| undefined)[] \| undefined`|
|select|选中日期发生改变但组件值未改变|value: `(Date \| string \| number \| undefined)[]`<br>date: `(Date \| undefined)[]`<br>dateString: `(string \| undefined)[]`|
|popup-visible-change|打开或关闭弹出框|visible: `boolean`|
|ok|点击确认按钮|value: `Date \| string \| number[]`<br>date: `Date[]`<br>dateString: `string[]`|
|clear|点击清除按钮|-|
|select-shortcut|点击快捷选项|shortcut: `ShortcutType`|
|picker-value-change|面板日期改变|value: `Date \| string \| number[]`<br>date: `Date[]`<br>dateString: `string[]`|




### ShortcutType

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|label|选项的内容|`string \| number \| (() => VNode)`|`-`|
|value|选项值|`(Date \| string \| number)    \| (Date \| string \| number)[]    \| (() => (Date \| string \| number) \| (Date \| string \| number)[])`|`-`|
|format|解析值所使用的格式，参考[字符串解析格式](#字符串解析格式)|`string`|`-`|



### 字符串解析格式

格式|输出|描述
---|---|---:
`YY`|21|两位数的年份
`YYYY`|2021|四位数年份
`M`|1-12|月份，从 1 开始
`MM`|01-12|月份，两位数
`MMM`|Jan-Dec|缩写的月份名称
`MMMM`|January-December|完整的月份名称
`D`|1-31|月份里的一天
`DD`|01-31|月份里的一天，两位数
`d`|0-6|一周中的一天，星期天是 0
`dd`|Su-Sa|最简写的一周中一天的名称
`ddd`|Sun-Sat|简写的一周中一天的名称
`dddd`|Sunday-Saturday|一周中一天的名称
`H`|0-23|小时
`HH`|00-23|小时，两位数
`h`|1-12|小时, 12 小时制
`hh`|01-12|小时, 12 小时制, 两位数
`m`|0-59|分钟
`mm`|00-59|分钟，两位数
`s`|0-59|秒
`ss`|00-59|秒，两位数
`S`|0-9|数百毫秒，一位数
`SS`|00-99|几十毫秒，两位数
`SSS`|000-999|毫秒，三位数字
`Z`|-5:00|UTC 的偏移量
`ZZ`|-0500|UTC 的偏移量，数字前面加上 0
`A`|AM PM|-
`a`|am pm|-
`Do`|1st... 3st|带序号的月份中的某天
`X`|1410715640.579|Unix 时间戳
`x`|1410715640579|Unix 毫秒时间戳

## FAQ

### 关于 `locale` 字段
可以使用组件库提供的语言包配置 `locale` 字段。
