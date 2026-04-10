---
name: arco-vue-form
description: "Arco Design Vue 表单 Form 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-form>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 表单 Form

来源组件：上游 `web-vue/components/form`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-form>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本用法

### 说明
表单的基本用法。




```vue
<template>
  <a-form :model="form" :style="{ width: '600px' }" @submit="handleSubmit">
    <a-form-item field="name" tooltip="Please enter username" label="Username">
      <a-input
        v-model="form.name"
        placeholder="please enter your username..."
      />
    </a-form-item>
    <a-form-item field="post" label="Post">
      <a-input v-model="form.post" placeholder="please enter your post..." />
    </a-form-item>
    <a-form-item field="isRead">
      <a-checkbox v-model="form.isRead"> I have read the manual </a-checkbox>
    </a-form-item>
    <a-form-item>
      <a-button html-type="submit">Submit</a-button>
    </a-form-item>
  </a-form>
  {{ form }}
</template>

<script>
import { reactive } from 'vue';

export default {
  setup() {
    const form = reactive({
      name: '',
      post: '',
      isRead: false,
    });
    const handleSubmit = (data) => {
      console.log(data);
    };

    return {
      form,
      handleSubmit,
    };
  },
};
</script>
```

## 示例：表单布局

### 说明
表单支持三种布局方式： `horizontal` - 水平排列 **（默认）**， `vertical` - 垂直排列， `inline` - 行内排列。




```vue
<template>
  <a-space direction="vertical" size="large" :style="{width: '600px'}">
    <a-radio-group v-model="layout" type="button">
      <a-radio value="horizontal">horizontal</a-radio>
      <a-radio value="vertical">vertical</a-radio>
      <a-radio value="inline">inline</a-radio>
    </a-radio-group>
    <a-form :model="form" :layout="layout">
      <a-form-item field="name" label="Username">
        <a-input v-model="form.name" placeholder="please enter your username..." />
      </a-form-item>
      <a-form-item field="post" label="Post">
        <a-input v-model="form.post" placeholder="please enter your post..." />
      </a-form-item>
      <a-form-item field="isRead">
        <a-checkbox v-model="form.isRead">
          I have read the manual
        </a-checkbox>
      </a-form-item>
      <a-form-item>
        <a-button>Submit</a-button>
      </a-form-item>
    </a-form>
    <div>
      {{ form }}
    </div>
  </a-space>
</template>

<script>
import { reactive, ref } from 'vue';

export default {
  setup() {
    const layout = ref('horizontal')
    const form = reactive({
      name: '',
      post: '',
      isRead: false,
    })

    return {
      layout,
      form,
    }
  },
}
</script>
```

## 示例：额外信息和帮助信息

### 说明
可以使用 `extra` 添加额外信息。
如果需要在外部自定义校验信息，可以使用 `help` 属性或插槽。设置 `help` 时校验信息会被屏蔽。




```vue
<template>
  <a-form :model="form" :style="{width:'600px'}">
    <a-form-item field="name" label="Username" validate-trigger="input" required>
      <a-input v-model="form.name" placeholder="please enter your username..." />
      <template #extra>
        <div>Used to login</div>
      </template>
    </a-form-item>
    <a-form-item field="post" label="Post" validate-trigger="input" required>
      <a-input v-model="form.post" placeholder="please enter your post..." />
      <template #extra>
        <div>Used to login</div>
      </template>
      <template #help>
        <div>Custom validate message</div>
      </template>
    </a-form-item>
    <a-form-item field="isRead">
      <a-checkbox v-model="form.isRead">
        I have read the manual
      </a-checkbox>
    </a-form-item>
  </a-form>
  {{ form }}
</template>

<script>
import { reactive } from 'vue';

export default {
  setup() {
    const form = reactive({
      name: '',
      post: '',
      isRead: false,
    })

    return {
      form,
    }
  },
}
</script>
```

## 示例：嵌套数据

### 说明
展示了多种表单项嵌套的方式。
表单项组件默认会将表单项状态和事件绑定到第一子组件，如果想要使用表单项进行布局设置，请设置 `:merge-props="false"` 以关闭绑定，或者使用函数指定需要绑定的数据。
如果使用 grid 组件进行布局，请设置 `:content-flex="false"` 关闭表单项内容的 flex 布局。




```vue
<template>
  <a-form :model="form" :style="{width:'600px'}">
    <a-form-item label="Username" :content-flex="false" :merge-props="false" extra="Show error message together">
      <a-row :gutter="8">
        <a-col :span="12">
          <a-form-item field="together.firstname" validate-trigger="input"
                       :rules="[{required:true,message:'firstname is required'}]" no-style>
            <a-input v-model="form.together.firstname" placeholder="please enter your firstname..." />
          </a-form-item>
        </a-col>
        <a-col :span="12">
          <a-form-item field="together.lastname" validate-trigger="input"
                       :rules="[{required:true,message:'lastname is required'}]" no-style>
            <a-input v-model="form.together.lastname" placeholder="please enter your lastname..." />
          </a-form-item>
        </a-col>
      </a-row>
    </a-form-item>
    <a-form-item label="Username" :content-flex="false" :merge-props="false">
      <a-row :gutter="8">
        <a-col :span="12">
          <a-form-item field="separate.firstname" validate-trigger="input"
                       extra="Show error message separate"
                       :rules="[{required:true,message:'firstname is required'}]" hide-label>
            <a-input v-model="form.separate.firstname" placeholder="please enter your firstname..." />
          </a-form-item>
        </a-col>
        <a-col :span="12">
          <a-form-item field="separate.lastname" validate-trigger="input"
                       :rules="[{required:true,message:'lastname is required'}]" hide-label>
            <a-input v-model="form.separate.lastname" placeholder="please enter your lastname..." />
          </a-form-item>
        </a-col>
      </a-row>
    </a-form-item>
    <a-form-item label="Posts" :content-flex="false" :merge-props="false">
      <a-space direction="vertical" fill>
        <a-form-item field="posts.post1" label="Post1">
          <a-input v-model="form.posts.post1" placeholder="please enter your post..." />
        </a-form-item>
        <a-form-item field="posts.post2" label="Post2">
          <a-input v-model="form.posts.post2" placeholder="please enter your post..." />
        </a-form-item>
      </a-space>
    </a-form-item>
    <a-form-item field="isRead">
      <a-checkbox v-model="form.isRead">
        I have read the manual
      </a-checkbox>
    </a-form-item>
  </a-form>
  {{ form }}
</template>

<script>
import { reactive } from 'vue';

export default {
  setup() {
    const form = reactive({
      together: {
        firstname: '',
        lastname: '',
      },
      separate: {
        firstname: '',
        lastname: '',
      },
      posts: {
        post1: '',
        post2: ''
      },
      isRead: false,
    })

    return {
      form,
    }
  },
}
</script>
```

## 示例：栅格布局

### 说明
展示了使用栅格布局的方式。可以使用 `label-col-flex` 属性指定标签的具体宽度。




```vue
<template>
  <a-form :model="form">
    <a-row :gutter="16">
      <a-col :span="8">
        <a-form-item field="value1" label="Value 1" label-col-flex="100px">
          <a-input v-model="form.value1" placeholder="please enter..." />
        </a-form-item>
      </a-col>
      <a-col :span="8">
        <a-form-item field="value2" label="Value 2" label-col-flex="80px">
          <a-input v-model="form.value2" placeholder="please enter..." />
        </a-form-item>
      </a-col>
      <a-col :span="8">
        <a-form-item field="value3" label="Value 3" label-col-flex="80px">
          <a-input v-model="form.value3" placeholder="please enter..." />
        </a-form-item>
      </a-col>
    </a-row>
    <a-row :gutter="16">
      <a-col :span="16">
        <a-form-item field="value4" label="Value 4" label-col-flex="100px">
          <a-input v-model="form.value4" placeholder="please enter..." />
        </a-form-item>
      </a-col>
      <a-col :span="8">
        <a-form-item field="value5" label="Value 5" label-col-flex="80px">
          <a-input v-model="form.value5" placeholder="please enter..." />
        </a-form-item>
      </a-col>
    </a-row>
  </a-form>
  {{ form }}
</template>

<script>
import { reactive } from 'vue';

export default {
  setup() {
    const form = reactive({
      value1: '',
      value2: '',
      value3: '',
      value4: '',
      value5: '',
    })

    return {
      form,
    }
  },
}
</script>
```

## 示例：自动标签宽度

### 说明
设置 `auto-label-width` 开启自动标签宽度。仅在 `layout="horizontal"` 布局下生效。
_* 目前仅在首次加载后生效。_




```vue
<template>
  <a-form :model="form" :style="{width:'600px'}" auto-label-width @submit="handleSubmit">
    <a-form-item field="name" label="Username">
      <a-input v-model="form.name" placeholder="please enter your username..." />
    </a-form-item>
    <a-form-item field="post" label="Post">
      <a-input v-model="form.post" placeholder="please enter your post..." />
    </a-form-item>
    <a-form-item field="isRead">
      <a-checkbox v-model="form.isRead">
        I have read the manual
      </a-checkbox>
    </a-form-item>
    <a-form-item>
      <a-button html-type="submit">Submit</a-button>
    </a-form-item>
  </a-form>
  {{ form }}
</template>

<script>
import { reactive } from 'vue';

export default {
  setup() {
    const form = reactive({
      name: '',
      post: '',
      isRead: false,
    })
    const handleSubmit = (data) => {
      console.log(data)
    }

    return {
      form,
      handleSubmit
    }
  },
}
</script>
```

## 示例：验证表单

### 说明
展示了表单校验的使用方法。




```vue
<template>
  <a-form ref="formRef" :size="form.size" :model="form" :style="{width:'600px'}" @submit="handleSubmit">
    <a-form-item field="size" label="Form Size" >
      <a-radio-group v-model="form.size" type="button">
        <a-radio value="mini">Mini</a-radio>
        <a-radio value="small">Small</a-radio>
        <a-radio value="medium">Medium</a-radio>
        <a-radio value="large">Large</a-radio>
      </a-radio-group>
    </a-form-item>
    <a-form-item field="name" label="Username"
                 :rules="[{required:true,message:'name is required'},{minLength:5,message:'must be greater than 5 characters'}]"
                 :validate-trigger="['change','input']"
    >
      <a-input v-model="form.name" placeholder="please enter your username..." />
    </a-form-item>
    <a-form-item field="age" label="Age"
                 :rules="[{required:true,message:'age is required'},{type:'number', max:200,message:'age is max than 200'}]"
    >
      <a-input-number v-model="form.age" placeholder="please enter your age..." />
    </a-form-item>
    <a-form-item field="section" label="Section" :rules="[{match:/section one/,message:'must select one'}]">
      <a-select v-model="form.section" placeholder="Please select ..." allow-clear>
        <a-option value="section one">Section One</a-option>
        <a-option value="section two">Section Two</a-option>
        <a-option value="section three">Section Three</a-option>
      </a-select>
    </a-form-item>
    <a-form-item field="province" label="Province" :rules="[{required:true,message:'province is required'}]">
      <a-cascader v-model="form.province" :options="options" placeholder="Please select ..." allow-clear />
    </a-form-item>
    <a-form-item field="options" label="Options"
                 :rules="[{type:'array',minLength:2,message:'must select greater than two options'}]"
    >
      <a-checkbox-group v-model="form.options">
        <a-checkbox value="option one">Section One</a-checkbox>
        <a-checkbox value="option two">Option Two</a-checkbox>
        <a-checkbox value="option three">Option Three</a-checkbox>
        <a-checkbox value="option four">Option Four</a-checkbox>
      </a-checkbox-group>
    </a-form-item>
    <a-form-item field="date" label="Date">
      <a-date-picker v-model="form.date" placeholder="Please select ..."/>
    </a-form-item>
    <a-form-item field="time" label="Time">
      <a-time-picker v-model="form.time" placeholder="Please select ..."/>
    </a-form-item>
    <a-form-item field="radio" label="Radio" :rules="[{match:/one/,message:'must select one'}]">
      <a-radio-group v-model="form.radio">
        <a-radio value="radio one">Radio One</a-radio>
        <a-radio value="radio two">Radio Two</a-radio>
      </a-radio-group>
    </a-form-item>
    <a-form-item field="slider" label="Slider" :rules="[{type:'number', min:5,message:'slider is min than 5'}]">
      <a-slider v-model="form.slider" :max="10" />
    </a-form-item>
    <a-form-item field="score" label="Score">
      <a-rate v-model="form.score" allow-clear />
    </a-form-item>
    <a-form-item field="switch" label="Switch" :rules="[{type:'boolean', true:true,message:'must be true'}]">
      <a-switch v-model="form.switch" />
    </a-form-item>
    <a-form-item field="multiSelect" label="Multiple Select">
      <a-select v-model="form.multiSelect" placeholder="Please select ..." multiple>
        <a-option value="section one">Section One</a-option>
        <a-option value="section two">Section Two</a-option>
        <a-option value="section three">Section Three</a-option>
      </a-select>
    </a-form-item>
    <a-form-item field="treeSelect" label="Tree Select">
      <a-tree-select :data="treeData" v-model="form.treeSelect" placeholder="Please select ..."/>
    </a-form-item>
    <a-form-item>
      <a-space>
        <a-button html-type="submit">Submit</a-button>
        <a-button @click="$refs.formRef.resetFields()">Reset</a-button>
      </a-space>
    </a-form-item>
  </a-form>
  {{ form }}
</template>

<script>
import { reactive } from 'vue';

export default {
  setup() {
    const handleSubmit = ({values, errors}) => {
      console.log('values:', values, '\nerrors:', errors)
    }

    const form = reactive({
      size: 'medium',
      name: '',
      age: undefined,
      section: '',
      province: 'haidian',
      options: [],
      date: '',
      time: '',
      radio: 'radio one',
      slider: 5,
      score: 5,
      switch: false,
      multiSelect: ['section one'],
      treeSelect: ''
    });
    const options = [
      {
        value: 'beijing',
        label: 'Beijing',
        children: [
          {
            value: 'chaoyang',
            label: 'ChaoYang',
            children: [
              {
                value: 'datunli',
                label: 'Datunli',
              },
            ],
          },
          {
            value: 'haidian',
            label: 'Haidian',
          },
          {
            value: 'dongcheng',
            label: 'Dongcheng',
          },
          {
            value: 'xicheng',
            label: 'XiCheng',
          },
        ],
      },
      {
        value: 'shanghai',
        label: 'Shanghai',
        children: [
          {
            value: 'shanghaishi',
            label: 'Shanghai',
            children: [
              {
                value: 'huangpu',
                label: 'Huangpu',
              },
            ],
          },
        ],
      },
    ];
    const treeData = [
      {
        key: 'node1',
        title: 'Node1',
        children: [
          {
            key: 'node2',
            title: 'Node2',
          },
        ],
      },
      {
        key: 'node3',
        title: 'Node3',
        children: [
          {
            key: 'node4',
            title: 'Node4',
          },
          {
            key: 'node5',
            title: 'Node5',
          },
        ],
      },
    ]

    return {
      form,
      options,
      treeData,
      handleSubmit
    }
  },
}
</script>
```

## 示例：验证表单2

### 说明
展示了表单校验`rules`使用在`a-form`上的使用方法，以及可以直接校验`email`、`ip`、`url`




```vue
<template>
  <a-form ref="formRef" :rules="rules" :model="form" :style="{width:'600px'}" @submit="handleSubmit">
    <a-form-item field="name" label="Username" validate-trigger="blur">
      <a-input v-model="form.name" placeholder="please enter your username..." />
    </a-form-item>
    <a-form-item field="password" label="密码" validate-trigger="blur">
      <a-input-password v-model="form.password" placeholder="please enter your password..." />
    </a-form-item>
    <a-form-item field="password2" label="确认密码" validate-trigger="blur">
      <a-input-password v-model="form.password2" placeholder="please confirm your password..." />
    </a-form-item>
    <a-form-item field="email" label="email">
      <a-input v-model="form.email" placeholder="please enter your email..." />
    </a-form-item>
    <a-form-item field="ip" label="IP">
      <a-input v-model="form.ip" placeholder="please enter your ip..." />
    </a-form-item>
    <a-form-item field="url" label="URL">
      <a-input v-model="form.url" placeholder="please enter your url..." />
    </a-form-item>
    <a-form-item field="match" label="match">
      <a-input v-model="form.match" placeholder="please enter your match..." />
    </a-form-item>
    <a-form-item>
      <a-space>
        <a-button html-type="submit">Submit</a-button>
        <a-button @click="$refs.formRef.resetFields()">Reset</a-button>
      </a-space>
    </a-form-item>
  </a-form>
  {{ form }}
</template>

<script>
import { reactive } from 'vue';

export default {
  setup() {
    const handleSubmit = ({values, errors}) => {
      console.log('values:', values, '\nerrors:', errors)
    }

    const form = reactive({
      name: '',
      password: '',
      password2: '',
      email: '',
      ip: '192.168.2.1',
      url: '',
      match: ''
    });

    const rules = {
      name: [
        {
          required: true,
          message:'name is required',
        },
      ],
      password: [
        {
          required: true,
          message:'password is required',
        },
      ],
      password2: [
        {
          required: true,
          message:'password is required',
        },
        {
          validator: (value, cb) => {
            if (value !== form.password) {
              cb('two passwords do not match')
            } else {
              cb()
            }
          }
        }
      ],
      email: [
        {
          type: 'email',
          required: true,
        }
      ],
      ip: [
        {
          type: 'ip',
          required: true,
        }
      ],
      url: [
        {
          type: 'url',
          required: true,
        }
      ],
      match: [
        {
          required: true,
          validator: (value, cb) => {
            return new Promise((resolve) => {
              if (!value) {
                cb('Please enter match')
              }
              if (value !== 'match') {
                cb('match must be match!')
              }
              resolve()
            })
          }
        }
      ],
    }

    return {
      form,
      rules,
      handleSubmit
    }
  },
}
</script>
```

## 示例：自定义表单校验状态

### 说明
开启 `feedback` 可以让部分输入组件展示当前状态信息




```vue
<template>
  <a-space direction="vertical" size="large">
    <a-radio-group v-model="status" type="button">
      <a-radio value="validating">validating</a-radio>
      <a-radio value="success">success</a-radio>
      <a-radio value="error">error</a-radio>
      <a-radio value="warning">warning</a-radio>
    </a-radio-group>
    <a-radio-group v-model="size" type="button">
      <a-radio value="mini">mini</a-radio>
      <a-radio value="small">small</a-radio>
      <a-radio value="medium">medium</a-radio>
      <a-radio value="large">large</a-radio>
    </a-radio-group>
  </a-space>
  <a-form
    :model="form"
    :style="{ width: '600px', marginTop: '20px' }"
    :size="size"
  >
    <a-form-item
      field="name"
      label="Username"
      help="This is custom message"
      extra="This is extra text"
      :validate-status="status"
      feedback
    >
      <a-input
        v-model="form.name"
        placeholder="please enter your username..."
      />
    </a-form-item>
    <a-form-item
      field="post"
      label="Post"
      help="This is custom message"
      extra="This is extra text"
      :validate-status="status"
      feedback
    >
      <a-input-number
        v-model="form.post"
        placeholder="please enter your post..."
      />
    </a-form-item>
    <a-form-item
      field="tags"
      label="Tags"
      help="This is custom message"
      extra="This is extra text"
      :validate-status="status"
      feedback
    >
      <a-input-tag
        v-model="form.tags"
        placeholder="please enter your post..."
      />
    </a-form-item>
    <a-form-item
      field="section"
      label="Section"
      :rules="[{ match: /section one/, message: 'must select one' }]"
      :validate-status="status"
      feedback
    >
      <a-select v-model="form.section" placeholder="Please select ...">
        <a-option value="section one">Section One</a-option>
        <a-option value="section two">Section Two</a-option>
        <a-option value="section three">Section Three</a-option>
      </a-select>
    </a-form-item>
    <a-form-item label="DateRange" :validate-status="status" feedback>
      <a-range-picker></a-range-picker>
    </a-form-item>

    <a-form-item field="date" label="Date" :validate-status="status" feedback>
      <a-date-picker></a-date-picker>
    </a-form-item>

    <a-form-item field="time" label="Time" :validate-status="status" feedback>
      <a-time-picker></a-time-picker>
    </a-form-item>
  </a-form>
</template>

<script>
import { reactive, ref } from 'vue';

export default {
  setup() {
    const status = ref('success');
    const size = ref('medium');
    const form = reactive({
      name: '',
      post: undefined,
      tags: ['tag1'],
      section: '',
    });

    return {
      status,
      size,
      form,
    };
  },
};
</script>
```

## 示例：动态表单

### 说明
通过数据动态控制表单内容。




```vue
<template>
  <a-form :model="form" :style="{width:'600px'}">
    <a-form-item field="name" label="Username">
      <a-input v-model="form.name" placeholder="please enter your username..." />
    </a-form-item>
    <a-form-item v-for="(post,index) of form.posts" :field="`posts[${index}].value`" :label="`Post-${index}`" :key="index">
      <a-input v-model="post.value" placeholder="please enter your post..." />
      <a-button @click="handleDelete(index)" :style="{marginLeft:'10px'}">Delete</a-button>
    </a-form-item>
  </a-form>
  <div>
    <a-button @click="handleAdd">Add Post</a-button>
  </div>
  {{ form }}
</template>

<script>
import { reactive } from 'vue';

export default {
  setup() {
    const form = reactive({
      name: '',
      posts: [{value: ''}]
    })
    const handleAdd = () => {
      form.posts.push({
        value: ''
      })
    };
    const handleDelete = (index) => {
      form.posts.splice(index, 1)
    }

    return {
      form,
      handleAdd,
      handleDelete
    }
  },
}
</script>
```

## 示例：全局禁用

### 说明
通过 `disabled` 属性可以禁用整个表单。




```vue
<template>
  <a-form :model="form" :style="{width:'600px'}" disabled>
    <a-form-item field="name" label="Username">
      <a-input v-model="form.name" placeholder="please enter your username..." />
    </a-form-item>
    <a-form-item field="post" label="Post">
      <a-input v-model="form.post" placeholder="please enter your post..." />
    </a-form-item>
    <a-form-item field="isRead">
      <a-checkbox v-model="form.isRead">
        I have read the manual
      </a-checkbox>
    </a-form-item>
    <a-form-item>
      <a-button>Submit</a-button>
    </a-form-item>
  </a-form>
  {{ form }}
</template>

<script>
import { reactive } from 'vue';

export default {
  setup() {
    const form = reactive({
      name: '',
      post: '',
      isRead: false,
    })

    return {
      form,
    }
  },
}
</script>
```

## 示例：表单异步校验

### 说明
通过异步的方法校验表单功能。




```vue

<template>
  <a-form ref="formRef" :model="form" :style="{width:'600px'}">
    <a-form-item field="name" label="Username" :rules="rules">
      <a-input v-model="form.name" placeholder="please enter your username..." />
    </a-form-item>
    <a-form-item field="post" label="Post">
      <a-input v-model="form.post" placeholder="please enter your post..." />
    </a-form-item>
    <a-form-item field="isRead">
      <a-checkbox v-model="form.isRead">
        I have read the manual
      </a-checkbox>
    </a-form-item>
    <a-form-item>
      <a-button @click="handleClick">Set Status</a-button>
    </a-form-item>
  </a-form>
  {{ form }}
</template>

<script>
import { ref, reactive } from 'vue';

export default {
  setup() {
    const formRef = ref()
    const form = reactive({
      name: '',
      post: '',
      isRead: false,
    })
    const rules = [{
      validator: (value, cb) => {
        return new Promise(resolve => {
          window.setTimeout(() => {
            if (value !== 'admin') {
              cb('name must be admin')
            }
            resolve()
          }, 2000)
        })
      }
    }];
    const handleClick = () => {
      formRef.value.setFields({
        name: {
          status: 'error',
          message: 'async name error'
        },
        post: {
          status: 'error',
          message: 'valid post'
        }
      })
    }

    return {
      formRef,
      form,
      rules,
      handleClick
    }
  },
}
</script>
```

## 示例：自定义表单组件

### 说明
通过 `useFormItem` 自定义表单组件。2.18.0 版本后可用。




```vue
<template>
  <a-space style="margin-bottom: 20px;">
    <a-switch v-model="disabled" />
    Disabled: {{disabled}}
  </a-space>
  <Form :model="form" :disabled="disabled" :style="{width:'600px'}">
    <FormItem field="name" label="Username"
              :rules="[{required:true,message:'name is required'},{minLength:5,message:'must be greater than 5 characters'}]">
      <MyInput v-model="form.name" placeholder="please enter your username..." />
    </FormItem>
  </Form>
</template>

<script lang="ts">
import { h, reactive, ref } from 'vue';
import { Form, FormItem, useFormItem } from '@arco-design/web-vue';

const MyInput = {
  emits: ['update:modelValue'],
  setup(_, { emit }) {
    const { mergedDisabled, eventHandlers } = useFormItem();
    const handleInput = (ev) => {
      const { value } = ev.target;
      emit('update:modelValue', value)
      eventHandlers.value?.onChange?.(ev)
    }
    return () => h('input', { disabled: mergedDisabled.value, onInput: handleInput })
  }
}

export default {
  components: {
    Form,
    FormItem,
    MyInput
  },
  setup() {
    const disabled = ref(false);
    const form = reactive({
      name: ''
    })

    return {
      disabled,
      form
    }
  },
}
</script>
```

## 示例：滚动到指定表单字段

### 说明
展示了提交失败自动滚动到第一个错误字段和手动滚动对应字段的使用方法。




```vue
<template>
  <a-space>
    <a-button @click="formRef && formRef.validate()">Submit</a-button>
    <a-button @click="formRef && formRef.resetFields()">Reset</a-button>
    <a-button @click="formRef && formRef.scrollToField('name19')">Scroll to the last field</a-button>
  </a-space>
  <a-form
    ref="formRef"
    style="width: 500px;height: 300px;margin-top:20px;padding-right: 16px;overflow: auto"
    :model="form"
    :scrollToFirstError="true"
  >
    <template v-for="(fieldName, index) in fieldNames" :key="index">
      <a-form-item
        :field="fieldName"
        :label="'user' + index"
        :rules="[
          { required: true, message: 'Name is required' },
        ]"
      >
        <a-input v-model="form[fieldName]" />
      </a-form-item>
    </template>
  </a-form>
</template>

<script>
import { reactive, ref } from 'vue';

export default {
  setup() {
    const formRef = ref(null);
    const fieldCount = 20;
    const fieldNames = Array.from({ length: fieldCount }, (_, index) => `name${index}`);
    const form = reactive(Object.fromEntries(
      fieldNames.map((fieldName, index) => [fieldName, index === 7 ? '' : index.toString()])
    ));

    return {
      form,
      formRef,
      fieldCount,
      fieldNames
    };
  },
};
</script>
```

## API


### `<form>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|model **(必填)**|表单数据对象|`object`|`-`||
|layout|表单的布局方式，包括水平、垂直、多列|`'horizontal' \| 'vertical' \| 'inline'`|`'horizontal'`||
|size|表单控件的尺寸|`'mini' \| 'small' \| 'medium' \| 'large'`|`'medium'`||
|label-col-props|标签元素布局选项。参数同 `<col>` 组件一致|`object`|` span: 5, offset: 0 `||
|wrapper-col-props|表单控件布局选项。参数同 `<col>` 组件一致|`object`|` span: 19, offset: 0 `||
|label-align|标签的对齐方向|`'left' \| 'right'`|`'right'`||
|disabled|是否禁用表单|`boolean`|`-`||
|rules|表单项校验规则|`Record<string, FieldRule \| FieldRule[]>`|`-`||
|auto-label-width|是否开启自动标签宽度，仅在 `layout="horizontal"` 下生效。|`boolean`|`false`|2.13.0|
|id|表单 `id` 属性和表单控件 `id` 前缀|`string`|`-`||
|scroll-to-first-error|验证失败后滚动到第一个错误字段|`boolean`|`false`|2.51.0|
### `<form>` 事件

|事件名|描述|参数|
|---|---|---|
|submit|表单提交时触发|data: `{values: Record<string, any>; errors: Record<string, ValidatedError> \| undefined}`<br>ev: `Event`|
|submit-success|验证成功时触发|values: `Record<string, any>`<br>ev: `Event`|
|submit-failed|验证失败时触发|data: `{values: Record<string, any>; errors: Record<string, ValidatedError>}`<br>ev: `Event`|
### `<form>` 方法

|方法名|描述|参数|返回值|版本|
|---|---|---|---|:---|
|validate|校验全部表单数据|callback: `(errors: undefined \| Record<string, ValidatedError>) => void`|Promise<undefined \| Record<string, ValidatedError>>||
|validateField|校验部分表单数据|field: `string \| string[]`<br>callback: `(errors: undefined \| Record<string, ValidatedError>) => void`|Promise<undefined \| Record<string, ValidatedError>>||
|resetFields|重置表单数据|field: `string \| string[]`|-||
|clearValidate|清除校验状态|field: `string \| string[]`|-||
|setFields|设置表单项的值和状态|data: `Record<string, FieldData>`|-||
|scrollToField|滚动到指定表单项|field: `string`|-|2.51.0|




### `<form-item>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|field|表单元素在数据对象中的path（数据项必填）|`string`|`''`||
|label|标签的文本|`string`|`-`||
|tooltip|提示内容|`string`|`-`|2.41.0|
|show-colon|是否显示冒号|`boolean`|`false`||
|no-style|是否去除样式|`boolean`|`false`||
|disabled|是否禁用|`boolean`|`-`||
|help|帮助文案|`string`|`-`||
|extra|额外显示的文案|`string`|`-`||
|required|是否必须填写|`boolean`|`false`||
|asterisk-position|可选择将星号置于 label 前/后|`'start' \| 'end'`|`'start'`|2.41.0|
|rules|表单项校验规则（优先级高于 form 的 rules）|`FieldRule \| FieldRule[]`|`-`||
|validate-status|校验状态|`'success' \| 'warning' \| 'error' \| 'validating'`|`-`||
|validate-trigger|触发校验的事件|`'change' \| 'input' \| 'focus' \| 'blur'`|`'change'`||
|label-col-props|标签元素布局选项。参数同 `<col>` 组件一致|`object`|`-`||
|wrapper-col-props|表单控件布局选项。参数同 `<col>` 组件一致|`object`|`-`||
|hide-label|是否隐藏标签|`boolean`|`false`||
|hide-asterisk|是否隐藏星号|`boolean`|`false`||
|label-col-style|标签元素布局组件的 style|`object`|`-`|2.10.0|
|wrapper-col-style|表单控件布局组件的 style|`object`|`-`|2.10.0|
|row-props|表单项布局选项。参数同 `<row>` 组件一致|`object`|`-`|2.10.0|
|row-class|表单项布局组件的 class|`string\|array\|object`|`-`|2.10.0|
|content-class|表单控件包裹层的 class|`string\|array\|object`|`-`|2.10.0|
|content-flex|内容层是否开启 flex 布局|`boolean`|`true`|2.13.0|
|merge-props|（已废除）控制传递到子元素上的 Props。默认包括 disabled、error、size、 events 和 FormItem 上的额外属性。2.18.0 版本废除|`boolean \| ((props: Record<string, any>) => Record<string, any>)`|`true`|2.13.0|
|label-col-flex|设置标签 `Col` 组件的 flex 属性。设置时表单 `Col` 组件的 flex 属性会被设置为 `auto`。|`number\|string`|`-`|2.13.0|
|feedback|是否显示表单控件的反馈图标|`boolean`|`false`|2.16.0|
|label-component|表单项标签渲染的元素|`string`|`'label'`|2.22.0|
|label-attrs|表单项元素的属性|`object`|`-`|2.22.0|
### `<form-item>` 插槽

|插槽名|描述|参数|
|---|:---:|---|
|label|标签|-|
|help|帮助信息|-|
|extra|额外内容|-|



## Type


### FieldRule

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|type|校验的值的类型，默认为 `'string'`|`'string'    \| 'number'    \| 'boolean'    \| 'array'    \| 'object'    \| 'email'    \| 'url'    \| 'ip'`|`-`|
|required|是否必填|`boolean`|`false`|
|message|校验失败时展示的信息|`string`|`-`|
|length|校验长度（string, array）|`number`|`-`|
|maxLength|最大长度（string）|`number`|`-`|
|minLength|最小长度（string）|`number`|`-`|
|match|匹配校验（string）|`RegExp`|`-`|
|uppercase|大写（string）|`boolean`|`false`|
|lowercase|小写（string）|`boolean`|`false`|
|min|最小值（number）|`number`|`-`|
|max|最大值（number）|`number`|`-`|
|equal|校验数值（number）|`number`|`-`|
|positive|正数（number）|`boolean`|`false`|
|negative|负数（number）|`boolean`|`false`|
|true|是否为 `true`（boolean）|`boolean`|`false`|
|false|是否为 `false`（boolean）|`boolean`|`false`|
|includes|数组中是否包含给定值（array）|`any[]`|`-`|
|deepEqual|数组元素是否相等（array）|`any`|`-`|
|empty|是否为空（object）|`boolean`|`false`|
|hasKeys|对象是否包含给定属性（object）|`string[]`|`-`|
|validator|自定义校验规则|`(    value: FieldValue \| undefined,    callback: (error?: string) => void  ) => void`|`-`|



### FieldData

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|value|字段的值|`any`|`-`|
|status|字段的状态|`ValidateStatus`|`-`|
|message|字段的错误信息|`string`|`-`|



### ValidatedError

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|label|标签的文本|`string`|`-`|2.18.0|
|field|字段名|`string`|`-`||
|value|字段值|`any`|`-`||
|type|字段类型|`string`|`-`||
|isRequiredError|是否为 `required` 错误|`boolean`|`false`||
|message|错误信息|`string`|`-`||



### FormItemEventHandler

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|onChange|onChange|`(ev?: Event) => void`|`-`|
|onInput|onInput|`(ev?: Event) => void`|`-`|
|onFocus|onFocus|`(ev?: Event) => void`|`-`|
|onBlur|onBlur|`(ev?: Event) => void`|`-`|



### useFormItem

```ts
const useFormItem = (data: {
  size?: Ref<Size | undefined>;
  disabled?: Ref<boolean>;
  error?: Ref<boolean>;
}) => {
  mergedSize:Ref<Size>;
  mergedDisabled:Ref<boolean>;
  mergedError:Ref<boolean>;
  feedback:Ref<string>;
  eventHandlers:Ref<FormItemEventHandler>;
}
```

## FAQ

### 关于 `form-item` 的 `field` 属性
`field` 属性的值为获取当前 `form-item` 对应值的路径字符串。

例如传入 model 属性的数据结构为：
```ts
const data = reactive({
  name:'xiaoming',
  people:[
    {
      id:'1111'
    },
    {
      // bind this value
      id:'2222'
    }
  ]
})
```
此时，如果想要指定当前 `form-item` 对应的值为 `id: '2222'`，需要设置 `field="people.1.id"`，值中的分隔符需要使用 `.`。数组分割也可以使用 `[]`，例如 `field="people[1].id"`

### 关于在 label 插槽中使用可点击元素

表单组件的标题区域默认使用 `label` 元素包裹，会在点击时激活输入组件，如果在其中放入可以点击组件，会影响其正常功能。
此时可以使用 `label-component` 属性修改包裹元素为 `span` 解决这个问题。
