## 简介

本项目为 opencc 的配置文件，功能是将中文转换为符号，如“平方”转换为 ² ，以此来实现输入法快速输入特殊符号。是为[🍀️四叶草简体拼音](https://github.com/fkxxyz/rime-cloverpinyin)而设计的。

## 安装

推荐直接使用[🍀️四叶草简体拼音](https://github.com/fkxxyz/rime-cloverpinyin)，自带该功能。

如果想要别的输入法带此功能，则按照下列步骤做：

确保自己机器上有 python 和 opencc

然后如下执行

```shell
./rime-symbols-gen
```

再将生成的所有文件复制到 rime 的目录的 opencc 子目录下（不存在就创建一个）

下面以 fcitx-rime 的用户配置文件为例

```shell
mkdir -p ~/.config/fcitx/rime/opencc
cp symbol_* ~/.config/fcitx/rime/opencc
```

然后给给自己的输入法打上 patch：

```yaml
patch:
  switches/@next:
    name: symbol_support
    reset: 1
    states: [ "无符", "符" ]
  'engine/filters/@before 0':
    simplifier@symbol_support
  symbol_support:
    opencc_config: symbol.json
    option_name: symbol_support
    tips: all
```

然后重新部署即可