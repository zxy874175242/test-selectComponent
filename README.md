# test-selectComponent

## `SelectPerson`组件

### 传入参数

- `resList`： 所有人员列表。

  ```json
  [
      {
          "name": "张三",
          "id": 1
      },
      {
          "name": "李四",
          "id": 2
      },
  ]
  ```

- `chosenList`： 初始选中人员id的数组，形如[1, 2, 3]。

### 效果展示

- 选择状态。点击蓝色圆形编辑按钮展开或收回选择面板，点击蓝色确定按钮可以收回选择面板。

  <img src="https://juanmdbucket.oss-cn-beijing.aliyuncs.com/20210311150148.png" alt="image-20210311150146807" style="zoom: 80%;" />

- 展示状态。

  ![image-20210311150308273](https://juanmdbucket.oss-cn-beijing.aliyuncs.com/20210311150310.png)

- 展示状态中可以进行删除，展⽰的已选中⼈员与选择⾯板中⼀致。

  ![image-20210311150558843](https://juanmdbucket.oss-cn-beijing.aliyuncs.com/20210311150600.png)

- 筛选功能。

  ![image-20210311150651623](https://juanmdbucket.oss-cn-beijing.aliyuncs.com/20210311150652.png)

