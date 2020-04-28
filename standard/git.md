# git 提交规范

```shell
npm install cz-customizable commitizen --save-dev
```

.

```json
//package.json
"config": {
  "commitizen": {
    "path": "node_modules/cz-customizable"
  }
}

```

```javascript
// .cz-config.js

module.exports = {
    types: [
        { value: '初次提交', name: ' 初次提交' },
        { value: '新功能', name: '新版本迭代，引入新功能' },
        { value: '修复bug', name: '修复:  修复一个Bug' },
        { value: '国际化', name: '国际化:  国际化与本地化' },
        { value: '文档', name: '文档:    变更的只有文档' },
        { value: '格式化', name: '格式:   空格, 分号等格式修复' },
        { value: '废弃删除', name: '格式:   移除废弃代码或文件' },
        { value: '重构', name: '重构:   代码重构，注意和特性、修复区分开' },
        { value: '性能', name: '性能:    提升代码性能' },
        { value: '测试', name: '测试:    添加一个测试' },
        { value: '工具', name: '工具:    开发工具变动(构建、脚手架工具等)' },
        { value: '回滚', name: '回滚:   代码回退' },
        { value: '依赖', name: '依赖:   升级依赖管理' }
    ],

    //范围
    //scope也为必填项，用于描述改动的范围，格式为项目名/模块名
    scopes: [
        { name: 'build' },
        { name: 'src/globe' },
        { name: 'src/view' },
        { name: 'src/router' },
        { name: 'src/bussnesscomp' },
        { name: 'src/component' }
    ],

    // it needs to match the value for field type. Eg.: 'fix'
    /*
  scopeOverrides: {
    fix: [
      {name: 'merge'},
      {name: 'style'},
      {name: 'e2eTest'},
      {name: 'unitTest'}
    ]
  },
  */
    // override the messages, defaults are as follows
    // body填写详细描述，主要描述改动之前的情况及修改动机，对于小的修改不作要求，但是重大需求、更新等必须添加body来作说明
    // break changes指明是否产生了破坏性修改，涉及break changes的改动必须指明该项，类似版本升级、接口参数减少、接口删除、迁移等。
    // 当前提交是针对特定的issue，那么可以在Footer部分填写需要关闭的单个 issue 或一系列issues。
    messages: {
        type: '选择一种你的提交类型:',
        scope: '选择一个scope (可选):',
        // used if allowCustomScopes is true
        customScope: 'Denote the SCOPE of this change:',
        subject: 'title说明:\n',
        body: '长说明，使用"|"换行(可选)：\n',
        breaking:
            '是否产生了破坏性修改，涉及break changes的改动必须指明该项，类似版本升级、接口参数减少、接口删除、迁移(可选):\n',
        footer: '关联关闭的issue，例如：#31, #34(可选):\n',
        confirmCommit: '确定提交说明?'
    },

    allowCustomScopes: true,
    allowBreakingChanges: ['特性', '修复'],

    // body  subject length
    subjectLimit: 100
};
```

## cz 提交代码

```shell
git cz
```
