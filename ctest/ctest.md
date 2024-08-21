# CTest入门

测试分类

- 冒烟测试 目的是对一个新编译需要正式测试的软件版本,确认软件的基本功能是正常的，可以进行后续的测试工作。
- 回归测试 重新测试之前测试的通过点。
- 黑盒测试 测试人只关注软件输入和输出，不考虑内部实现细节。
- 白盒测试 测试软件内部架构和设计

## CTest

```cmake
# 使能测试
enable_testing()
# 包含测试模块
include(CTest)
```

- add_test(NAME TestName COMMAND ExecutableToRun arg1 arg2 ...)
  - TestName 名称
  - ExecutableToRun 可执程序名称
  - arg1 arg2 运行参数
- 测试特性
  - 默认测试特性:
    - 测试执行程序找到
    - 测试程序无异常
    - 测试程序返回 **0**
  - set_property(TEST test_name PROPERTY prop1 value1 value2 ...) 设置测试特性
    - ENVIRONMENT 设置测试环境变量
    - 指定与测试关联的文本标签
    - WILL_FAIL  返回不为 **0** 通过，反之失败
    - PASS_REGULAR_EXPRESSION 根据正则表达式检测输出结果为 **pass**
    - FAIL_REGULAR_EXPRESSION 根据正则表达式检测输出结果为 **fail**

```cmake
set (passRegex "^Test passed" "^All ok")
set (failRegex "Error" "Fail")

set_property (TEST outputTest
              PROPERTY PASS_REGULAR_EXPRESSION "${passRegex}")
set_property (TEST outputTest
              PROPERTY FAIL_REGULAR_EXPRESSION "${failRegex}")
```

### ExternalData 外部管理数据集
