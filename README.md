# OSSDP-Lab2

本仓库包含 Lab2 的题目文件；本次修复与单元测试的对象为第 9 题 `possibleBipartition`。

## 运行第 9 题测试

准备 JDK 17 或更高版本，确保 `java`、`javac` 和 `curl` 可用。测试类为
`L2024130080_9_Test`，使用 JUnit 4；下面的 JUnit Platform Console Standalone
1.11.4 包含运行该测试所需的 JUnit Vintage 引擎与 JUnit 4 支持。

在仓库根目录使用 macOS 或 Linux 的 shell 执行以下命令。依赖和编译结果放入新建的临时目录，
不会在仓库中生成 JAR 或 class 文件。

```sh
lab2_test_dir=$(mktemp -d)
junit_jar="$lab2_test_dir/junit-platform-console-standalone-1.11.4.jar"

curl --fail --location --output "$junit_jar" \
  https://repo.maven.apache.org/maven2/org/junit/platform/junit-platform-console-standalone/1.11.4/junit-platform-console-standalone-1.11.4.jar

mkdir -p "$lab2_test_dir/classes"
javac --release 17 -encoding UTF-8 -cp "$junit_jar" \
  -d "$lab2_test_dir/classes" Solution9.java L2024130080_9_Test.java

java -jar "$junit_jar" execute \
  --class-path "$lab2_test_dir/classes" \
  --select-class L2024130080_9_Test \
  --fail-if-no-tests
```

这里只编译第 9 题的源文件和测试类，其余题目保留教师原始代码，不应一并加入本次编译。
`--select-class` 明确选择测试类，`--fail-if-no-tests` 保证未发现测试时返回失败状态。
测试完成后可删除 `$lab2_test_dir` 指向的临时目录。

## 测试覆盖与核验

现有测试覆盖题目示例、空图、最大编号顶点、链、星形、奇偶环、完全二分图、多个连通分量、
较大规模输入，以及固定随机种子生成的 500 个图与独立 BFS 染色实现的对照。

2026 年 11 月 28 日，基于提交 `24be7ac`，使用 Temurin JDK 21、Java 17 编译目标和
JUnit Platform Console Standalone 1.11.4 验证：16 个测试全部通过，0 个失败。
