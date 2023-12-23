# dict-database

词典数据库

## 简介

该项目提供了 sql 格式的词典，需要词典数据库的开发者自行下载相关文件。

## 简明英汉汉英词典

该词典数据来自"简明英汉汉英词典.mdx"。词条总数差不多 115 万。

该词典包含单词、短语、中文词组。其中，中文词组差不多十万条，位于记录的最后面。

### sql

因为单词的每行释义拆分成了一条记录，所以 words 表总记录差不多 117 万。

我服务器 mysql 版本是 5.7，可以导入。后来试了 8.x 版本，通过 myPhpAdmin 导入的，没有发现文件错误，因为内存耗尽了。建议还是命令行导入吧。

| 表名称   | 说明     |
| -------- | -------- |
| metainfo | 词典信息 |
| words    | 词条     |
| examples | 例句     |

![截图](./assets/images/%E7%AE%80%E6%98%8E%E8%8B%B1%E6%B1%89%E6%B1%89%E8%8B%B1%E8%AF%8D%E5%85%B8-%E6%88%AA%E5%9B%BE.jpg)

### json

sql 格式限制有点多，所以又生成了 json 版本。json 版本示例如下：

```json
{
  "info": {
    // 词典头信息
    "header": {
      // 这里示例省略
    },
    "keyHeader": {
      "keyBlocksNum": 877,
      "entriesNum": 1155424,
      "keyBlockInfoDecompSize": 54794,
      "keyBlockInfoCompSize": 22140,
      "keyBlocksTotalSize": 10261871
    },
    "recordHeader": {
      "recordBlocksNum": 6755,
      "entriesNum": 1155424,
      "recordBlockInfoCompSize": 108080,
      "recordBlockCompSize": 34465405
    }
  },
  // 记录
  "records": [
    {
      "word": "the", // 单词
      "sections": [ // 部分单词有多种读音，所以统一分段
        {
          "phonetic": [ // 音标
            "D.J.:[ðə]",
            "K.K.:[ði,ðə]"
          ],
          "partsOfSpeech": [
            {
              "partOfSpeech": "art.", // 词性
              "definitions": [ // 定义
                {
                  "definition": "(指已提到的人[物])",
                  "examples": [ // 示例
                    {
                      "origin": "It's her room.The room is bright and clean.",
                      "translation": "这是她的房间。这房间明亮整洁。"
                    }
                  ]
                },
              ]
            }
          ]
        }
      ]
    }
  ]
}
```

## 中华成语大词典

该词典数据来自“中华成语大词典.mdx”。将近 5 万个词条。

仅提供 json 格式。

```json
{
  "info": {
    // 词典头信息
    "header": {
    },
    "keyHeader": {
      "keyBlocksNum": 33,
      "entriesNum": 49838,
      "keyBlockInfoDecompSize": 1864,
      "keyBlockInfoCompSize": 952,
      "keyBlocksTotalSize": 507905
    },
    "recordHeader": {
      "recordBlocksNum": 696,
      "entriesNum": 49838,
      "recordBlockInfoCompSize": 11136,
      "recordBlockCompSize": 10041333
    }
  },
  // 字典拼音索引
  "indices": [
    {
      "word": "a",
      "items": [
        "阿鼻地狱",
        "阿鼻叫唤",
        "阿斗太子",
        "阿狗阿猫",
        "阿姑阿翁",
        "阿家阿翁",
        "阿娇金屋",
        "阿猫阿狗",
        "阿毗地狱",
        "阿平绝倒"
      ]
    },
  ],
  /**
   * 记录--不是每个词条都拥有完整的内容
   * 字段：
   *   解释: "definition",
   *   出处: "source",
   *   示例: "example",
   *   近义词: "synonyms",
   *   反义词: "antonyms",
   *   歇后语: "wisecrack",
   *   语法: "grammar",
   *   英文: "english",
   *   日文: "japanese",
   *   德文: "german",
   *   法文: "franch",
   *   俄文: "russian",
   *   汉语: "korean",
   *   成语故事: "story",
   */
  "records": [
    {
      "word": "一丁不识",
      "phonetic": "yī  dīng  bù  shí", // 拼音
      "definition": "形容一个字也不认识。",
      "source": "《旧唐书·张弘靖传》：“天下无事，汝辈挽得两石弓，不如识一丁字。”",
      "example": "而云古无类书，此真～之无知妄作也矣。 ★清·平步青《霞外捃屑》卷七",
      "synonyms": "目不识丁",
      "antonyms": "学富五车",
      "grammar": "作谓语、定语；指不识字",
      "english": "not know one's ABC"
    },
  ]
}
```
