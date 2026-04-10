---
name: arco-vue-upload
description: "Arco Design Vue 上传 Upload 组件参考。用于 Vue 3、`@arco-design/web-vue`、`<a-upload>`、属性、事件、插槽、示例和实现细节。"
user-invocable: false
---

# 上传 Upload

来源组件：上游 `web-vue/components/upload`

## Vue 使用要点

- 优先使用 Vue 3 Composition API 和 `<script setup lang="ts">`。
- 完整注册 `app.use(ArcoVue)` 后，默认使用 `<a-upload>` 形式的全局组件标签；也可以从 `@arco-design/web-vue` 按需导入组件并局部注册。
- 模板中的属性使用 kebab-case，例如 `html-type`、`show-jumper`、`row-selection`。
- 双向绑定使用 `v-model` 或组件文档中说明的命名形式，例如 `v-model:visible`。
- 事件使用 `@event-name`，插槽使用 `#slot-name`，作用域插槽参数以组件 API 表为准。

## 示例：基本使用

### 说明
上传组件的基本用法。




```vue
<template>
  <a-space direction="vertical" :style="{ width: '100%' }">
    <a-upload action="/" />
    <a-upload action="/" disabled style="margin-top: 40px;"/>
  </a-space>
</template>
```

## 示例：用户头像上传

### 说明
点击上传用户头像，可使用 beforeUpload 限制用户上传的图片格式和大小。




```vue

<template>
  <a-space direction="vertical" :style="{ width: '100%' }">
    <a-upload
      action="/"
      :fileList="file ? [file] : []"
      :show-file-list="false"
      @change="onChange"
      @progress="onProgress"
    >
      <template #upload-button>
        <div
          :class="`arco-upload-list-item${
            file && file.status === 'error' ? ' arco-upload-list-item-error' : ''
          }`"
        >
          <div
            class="arco-upload-list-picture custom-upload-avatar"
            v-if="file && file.url"
          >
            <img :src="file.url" />
            <div class="arco-upload-list-picture-mask">
              <IconEdit />
            </div>
            <a-progress
              v-if="file.status === 'uploading' && file.percent < 100"
              :percent="file.percent"
              type="circle"
              size="mini"
              :style="{
                position: 'absolute',
                left: '50%',
                top: '50%',
                transform: 'translateX(-50%) translateY(-50%)',
              }"
            />
          </div>
          <div class="arco-upload-picture-card" v-else>
            <div class="arco-upload-picture-card-text">
              <IconPlus />
              <div style="margin-top: 10px; font-weight: 600">Upload</div>
            </div>
          </div>
        </div>
      </template>
    </a-upload>
  </a-space>
</template>

<script>
import { IconEdit, IconPlus } from '@arco-design/web-vue/es/icon';
import { ref } from 'vue';

export default {
  components: {IconPlus, IconEdit},
  setup() {
    const file = ref();

    const onChange = (_, currentFile) => {
      file.value = {
        ...currentFile,
        // url: URL.createObjectURL(currentFile.file),
      };
    };
    const onProgress = (currentFile) => {
      file.value = currentFile;
    };
    return {
      file,
      onChange,
      onProgress
    }
  },
};
</script>
```

## 示例：已上传的文件列表

### 说明
可以指定默认的已上传文件列表。




```vue
<template>
  <a-upload action="/" :default-file-list="fileList" />
</template>

<script>
export default {
  setup() {
    const fileList = [
      {
        uid: '-1',
        name: 'ice.png',
        url: '//p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/3ee5f13fb09879ecb5185e440cef6eb9.png~tplv-uwbnlip3yd-webp.webp',
      },
      {
        status: 'error',
        uid: '-2',
        percent: 0,
        response: '上传错误提示',
        name: 'cat.png',
        url: '//p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/e278888093bef8910e829486fb45dd69.png~tplv-uwbnlip3yd-webp.webp',
      },
      {
        uid: '-3',
        name: 'light.png',
        url: '//p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/a8c8cdb109cb051163646151a4a5083b.png~tplv-uwbnlip3yd-webp.webp',
      },
    ];

    return {
      fileList
    }
  },
};
</script>
```

## 示例：照片墙

### 说明
通过设置 `list-type="picture-card"` 开启照片墙模式。




```vue
<template>
  <a-upload
    list-type="picture-card"
    action="/"
    :default-file-list="fileList"
    image-preview
  />
</template>

<script>
export default {
  setup() {
    const fileList = [
      {
        uid: '-2',
        name: '20200717-103937.png',
        url: '//p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/a8c8cdb109cb051163646151a4a5083b.png~tplv-uwbnlip3yd-webp.webp',
      },
      {
        uid: '-1',
        name: 'hahhahahahaha.png',
        url: '//p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/e278888093bef8910e829486fb45dd69.png~tplv-uwbnlip3yd-webp.webp',
      },
    ];

    return {
      fileList
    }
  },
};
</script>
```

## 示例：拖拽上传

### 说明
通过设置 `draggable` 开启对拖拽的支持。




```vue
<template>
  <a-upload draggable action="/" />
</template>
```

## 示例：图标列表样式

### 说明
通过设置 `list-type="picture"` 开启图片列表样式




```vue
<template>
  <a-upload
    list-type="picture"
    action="/"
    :default-file-list="fileList"
  />
</template>

<script>
export default {
  setup() {
    const fileList = [
      {
        uid: '-2',
        name: '20200717-103937.png',
        url: '//p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/a8c8cdb109cb051163646151a4a5083b.png~tplv-uwbnlip3yd-webp.webp',
      },
      {
        uid: '-1',
        name: 'hahhahahahaha.png',
        url: '//p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/e278888093bef8910e829486fb45dd69.png~tplv-uwbnlip3yd-webp.webp',
      },
    ];

    return {
      fileList
    }
  },
};
</script>
```

## 示例：手动上传

### 说明
设置 `auto-upload` 为 `false` 时候，可以通过调用 `submit` 方法进行手动上传。




```vue
<template>
  <div>
    <a-upload
      action="/"
      :auto-upload="false"
      ref="uploadRef"
      @change="onChange"
      multiple
    >
      <template #upload-button>
        <a-space>
          <a-button> select file</a-button>
          <a-button type="primary" @click="submit"> start upload</a-button>
          <a-button type="primary" @click="submitOne">
            only upload one
          </a-button>
        </a-space>
      </template>
    </a-upload>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const uploadRef = ref();
    const files = ref([]);

    const submitOne = (e) => {
      e.stopPropagation();
      console.log(files.value);
      uploadRef.value.submit(files.value.find((x) => x.status === 'init'));
    };

    const submit = (e) => {
      e.stopPropagation();
      uploadRef.value.submit();
    };

    const onChange = (fileList) => {
      files.value = fileList;
    };

    return {
      uploadRef,
      files,
      submitOne,
      submit,
      onChange,
    };
  },
};
</script>
```

## 示例：上传前校验

### 说明
`beforeUpload` 会在每一个文件上传之前执行。如果返回 `false` 或者` Promise.reject`， 那么将会取消当前文件的上传。




```vue
<template>
  <a-space direction="vertical" :style="{ width: '100%' }">
    <a-upload action="/" @before-upload="beforeUpload" />
  </a-space>
</template>

<script>
import { Modal } from '@arco-design/web-vue';

export default {
  setup() {
    const beforeUpload = (file) => {
      return new Promise((resolve, reject) => {
        Modal.confirm({
          title: 'beforeUpload',
          content: `确认上传 ${file.name}`,
          onOk: () => resolve(true),
          onCancel: () => reject('cancel'),
        });
      });
    };
    return {
      beforeUpload
    }
  },
};
</script>
```

## 示例：移除前校验

### 说明
`on-before-remove` 会在每一个文件移除之前执行。如果返回 `false` 或者` Promise.reject`， 那么将会取消当前文件的操作。




```vue
<template>
  <a-space direction="vertical" :style="{ width: '100%' }">
    <a-upload
      action="/"
      :default-file-list="[
        {
          uid: '-2',
          name: 'light.png',
          url: '//p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/a8c8cdb109cb051163646151a4a5083b.png~tplv-uwbnlip3yd-webp.webp',
        },
        {
          uid: '-1',
          name: 'ice.png',
          url: '//p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/3ee5f13fb09879ecb5185e440cef6eb9.png~tplv-uwbnlip3yd-webp.webp',
        },
      ]"
      @before-remove="beforeRemove"
    />
  </a-space>
</template>

<script>
import { Modal } from '@arco-design/web-vue';

export default {
  setup() {
    const beforeRemove = (file) => {
      return new Promise((resolve, reject) => {
        Modal.confirm({
          title: 'on-before-remove',
          content: `确认删除 ${file.name}`,
          onOk: () => resolve(true),
          onCancel: () => reject('cancel'),
        });
      });
    };

    return {
      beforeRemove
    }
  },
};
</script>
```

## 示例：限制上传数量

### 说明
通过 `limit` 限制上传的最大数量。超出后上传按钮会隐藏.




```vue
<template>
  <a-upload multiple action="/" :limit="3" />
</template>
```

## 示例：自定义上传节点

### 说明
可以通过插槽 `upload-button` 传入自定义内容作为文件上传的触发节点。




```vue
<template>
  <a-upload action="/">
    <template #upload-button>
      <div
        style="
        background-color: var(--color-fill-2);
        color: var(--color-text-1);
        border: 1px dashed var(--color-fill-4);
        height: 158px;
        width: 380px;
        border-radius: 2;
        line-height: 158px;
        text-align: center;"
      >
        <div>
          Drag the file here or
          <span style="color: #3370FF"> Click to upload</span>
        </div>
      </div>
    </template>
  </a-upload>
</template>
```

## 示例：自定义图标

### 说明
自定义图标




```vue

<template>
  <div>
    <div style="margin-bottom: 20px;">
      <a-space>
        <span>Type: </span>
        <a-radio-group v-model="type">
          <a-radio value="text">text</a-radio>
          <a-radio value="picture">picture</a-radio>
          <a-radio value="picture-card">picture-card</a-radio>
        </a-radio-group>
      </a-space>
    </div>
    <a-upload
      action="/"
      :list-type="type"
      :default-file-list="[
        {
          uid: '-1',
          name: 'ice.png',
          url: '//p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/3ee5f13fb09879ecb5185e440cef6eb9.png~tplv-uwbnlip3yd-webp.webp',
        },
        {
          uid: '-3',
          name: 'light.png',
          url: '//p1-arco.byteimg.com/tos-cn-i-uwbnlip3yd/a8c8cdb109cb051163646151a4a5083b.png~tplv-uwbnlip3yd-webp.webp',
        },
      ]"
      :custom-icon="getCustomIcon()"
    />
  </div>
</template>

<script>
import { h, ref } from 'vue';
import { IconUpload, IconFileAudio, IconClose, IconFaceFrownFill } from '@arco-design/web-vue/es/icon';

export default {
  setup() {
    const type = ref('text');
    const getCustomIcon = () => {
      return {
        retryIcon: () => h(IconUpload),
        cancelIcon: () => h(IconClose),
        fileIcon: () => h(IconFileAudio),
        removeIcon: () => h(IconClose),
        errorIcon: () => h(IconFaceFrownFill),
        fileName: (file) => {
          return `文件名： ${file.name}`
        },
      };
    };

    return {
      type,
      getCustomIcon
    }
  },
};
</script>
```

## 示例：自定义上传请求

### 说明
可以通过 `custom-request` 实现自定义上传请求。




```vue
<template>
  <a-upload :custom-request="customRequest" />
</template>

<script>
export default {
  setup() {
    const customRequest = (option) => {
      const {onProgress, onError, onSuccess, fileItem, name} = option
      const xhr = new XMLHttpRequest();
      if (xhr.upload) {
        xhr.upload.onprogress = function (event) {
          let percent;
          if (event.total > 0) {
            // 0 ~ 1
            percent = event.loaded / event.total;
          }
          onProgress(percent, event);
        };
      }
      xhr.onerror = function error(e) {
        onError(e);
      };
      xhr.onload = function onload() {
        if (xhr.status < 200 || xhr.status >= 300) {
          return onError(xhr.responseText);
        }
        onSuccess(xhr.response);
      };

      const formData = new FormData();
      formData.append(name || 'file', fileItem.file);
      xhr.open('post', '//upload-z2.qbox.me/', true);
      xhr.send(formData);

      return {
        abort() {
          xhr.abort()
        }
      }
    };

    return {
      customRequest
    }
  },
}
</script>
```

## 示例：文件夹上传

### 说明
可以通过 `directory` 开启文件夹上传




```vue
<template>
  <a-space direction="vertical" :style="{ width: '100%' }">
    <a-upload action="/" directory />
  </a-space>
</template>
```

## API


### `<upload>` 属性

|参数名|描述|类型|默认值|版本|
|---|---|---|:---:|:---|
|file-list **(v-model)**|文件列表|`FileItem[]`|`-`||
|default-file-list|默认的文件列表（非受控状态）|`FileItem[]`|`[]`||
|accept|接收的上传文件类型，具体参考 [HTML标准](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/file#htmlattrdefaccept "_blank")|`string`|`-`||
|action|上传的URL|`string`|`-`||
|disabled|是否禁用|`boolean`|`false`||
|multiple|是否支持多文件上传|`boolean`|`false`||
|directory|是否支持文件夹上传（需要浏览器支持）|`boolean`|`false`||
|draggable|是否支持拖拽上传|`boolean`|`false`||
|tip|提示文字|`string`|`-`||
|headers|上传请求附加的头信息|`Record<string, string>`|`-`||
|data|上传请求附加的数据|`Record<string, string \| Blob>\| ((fileItem: FileItem) => Record<string, string \| Blob>)`|`-`||
|name|上传的文件名|`string \| ((fileItem: FileItem) => string)`|`-`||
|with-credentials|上传请求是否携带 cookie|`boolean`|`false`||
|custom-request|自定义上传行为|`(option: RequestOption) => UploadRequest`|`-`||
|limit|限制上传文件的数量。`0`表示不限制|`number`|`0`||
|auto-upload|是否自动上传文件|`boolean`|`true`||
|show-file-list|是否显示文件列表|`boolean`|`true`||
|show-remove-button|是否显示删除按钮|`boolean`|`true`|2.11.0|
|show-retry-button|是否显示重试按钮|`boolean`|`true`|2.11.0|
|show-cancel-button|是否显示取消按钮|`boolean`|`true`|2.11.0|
|show-upload-button|是否显示上传按钮。2.14.0 版本新增 `showOnExceedLimit` 支持|`boolean \| { showOnExceedLimit: boolean }`|`true`|2.11.0|
|show-preview-button|照片墙是否显示预览按钮|`boolean`|`true`|2.42.0|
|download|是否在 `<a>` 链接上添加 download 属性|`boolean`|`false`|2.11.0|
|show-link|在列表模式下，如果上传的文件存在 URL 则展示链接。如果关闭仅展示文字并且点击可以触发 `preview` 事件。|`boolean`|`true`|2.13.0|
|image-loading|`<img>` 的原生 HTML 属性，需要浏览器支持|`'eager' \| 'lazy'`|`-`|2.11.0|
|list-type|图片列表类型|`'text' \| 'picture' \| 'picture-card'`|`'text'`||
|response-url-key|Response中获取图片URL的key，开启后会用上传的图片替换预加载的图片|`string \| ((fileItem: FileItem) => string)`|`-`||
|custom-icon|自定义图标|`CustomIcon`|`-`||
|image-preview|是否使用 ImagePreview 组件进行预览|`boolean`|`false`|2.14.0|
|on-before-upload|上传文件前触发|`(file: File) => boolean \| Promise<boolean \| File>`|`-`||
|on-before-remove|移除文件前触发|`(fileItem: FileItem) => Promise<boolean>`|`-`||
|on-button-click|点击上传按钮触发（如果返回 Promise 则会关闭默认 input 上传）|`(event: Event) => Promise<FileList> \| void`|`-`||
### `<upload>` 事件

|事件名|描述|参数|
|---|---|---|
|exceed-limit|上传的文件超出限制后触发|fileList: `FileItem[]`<br>files: `File[]`|
|change|上传的文件状态发生改变时触发|fileList: `FileItem[]`<br>fileItem: `fileItem`|
|progress|上传中的文件进度改变时触发|fileItem: `fileItem`<br>ev: `ProgressEvent`|
|preview|点击图片预览时的触发|fileItem: `FileItem`|
|success|上传成功时触发|fileItem: `FileItem`|
|error|上传失败时触发|fileItem: `FileItem`|
### `<upload>` 方法

|方法名|描述|参数|返回值|版本|
|---|---|---|---|:---|
|submit|上传文件（已经初始化完成的文件）|fileItem: `FileItem`|-||
|abort|中止上传|fileItem: `FileItem`|-||
|updateFile|更新文件|id: `string`<br>file: `File`|-||
|upload|上传文件|files: `File[]`|-|2.41.0|
### `<upload>` 插槽

|插槽名|描述|参数|版本|
|---|:---:|---|:---|
|extra-button|上传列表额外按钮|fileItem: `FileItem`|2.43.0|
|image|自定义图片|fileItem: `FileItem`|2.23.0|
|file-name|文件名称|-|2.23.0|
|file-icon|文件图标|-|2.23.0|
|remove-icon|删除图标|-|2.23.0|
|preview-icon|预览图标|-|2.23.0|
|cancel-icon|取消图标|-|2.23.0|
|start-icon|开始图标|-|2.23.0|
|error-icon|失败图标|-|2.23.0|
|success-icon|成功图标|-|2.23.0|
|retry-icon|重试图标|-|2.23.0|
|upload-button|上传按钮|-||
|upload-item|上传列表的项目|fileItem: `FileItem`<br>index: `number`||




### FileItem

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|uid|当前上传文件的唯一标示|`string`|`-`|
|status|当前上传文件的状态|`FileStatus`|`-`|
|file|文件对象|`File`|`-`|
|percent|上传进度百分比|`number`|`-`|
|response|当前文件上传请求返回的响应|`any`|`-`|
|url|文件地址|`string`|`-`|
|name|文件名|`string`|`-`|



### CustomIcon

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|startIcon|开始图标|`RenderFunction`|`-`|
|cancelIcon|取消图标|`RenderFunction`|`-`|
|retryIcon|重试图标|`RenderFunction`|`-`|
|successIcon|成功图标|`RenderFunction`|`-`|
|errorIcon|失败图标|`RenderFunction`|`-`|
|removeIcon|移除图标|`RenderFunction`|`-`|
|previewIcon|预览图标|`RenderFunction`|`-`|
|fileIcon|文件图标|`(fileItem: FileItem) => VNode`|`-`|
|fileName|文件名|`(fileItem: FileItem) => string \| VNode`|`-`|



### RequestOption

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|action|上传的URL|`string`|`-`|
|headers|请求报文的头信息|`Record<string, string>`|`-`|
|name|上传文件的文件名|`string \| ((fileItem: FileItem) => string)`|`-`|
|fileItem|上传文件|`FileItem`|`-`|
|data|附加的请求信息|`Record<string, string \| Blob>    \| ((fileItem: FileItem) => Record<string, string \| Blob>)`|`-`|
|withCredentials|是否携带cookie信息|`boolean`|`false`|
|onProgress|更新当前文件的上传进度。percent: 当前上传进度百分比|`(percent: number, event?: ProgressEvent) => void`|`-`|
|onSuccess|上传成功后，调用onSuccess方法，传入的response参数将会附加到当前上传文件的response字段上|`(response?: any) => void`|`-`|
|onError|上传失败后，调用onError方法，传入的response参数将会附加到当前上传文件的response字段上|`(response?: any) => void`|`-`|



### UploadRequest

|参数名|描述|类型|默认值|
|---|---|---|:---:|
|abort|终止上传|`() => void`|`-`|
