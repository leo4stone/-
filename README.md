# 中华人民共和国职业分类大典 JSON 数据

## 项目介绍

本项目旨在将《中华人民共和国职业分类大典（2022年版）社会公示稿》中的职业分类数据整理为结构化的JSON格式，方便开发者、研究人员和相关机构进行数据分析、应用开发和研究工作。

通过将文档版本的职业分类大典转换为JSON数据，我希望能够：

- 提高数据的可访问性和可用性
- 便于程序化处理和分析
- 支持相关应用和系统的开发
- 促进职业分类标准的推广和应用

## 数据来源

数据来源于《中华人民共和国职业分类大典（2022年版）社会公示稿》。该分类大典是由人力资源和社会保障部组织编制的国家职业分类标准，对我国职业进行了系统的分类和描述。

## 文件说明

本项目包含以下文件：

- `01_职业分类大典2022.txt` - 从PDF提取的文本内容，保留了原始格式
- `02_职业分类大典2022_index.txt` - 职业分类的树状索引结构，便于快速浏览
- `03_职业分类大典2022.json` - 扁平化的JSON数据，包含所有职业信息
- `04_职业分类大典2022_hierarchical.json` - 层次化的JSON数据，保留了职业分类的嵌套结构

## 数据结构

### 扁平化JSON格式 (03_职业分类大典2022.json)

数据以JSON数组形式组织，每个职业信息包含以下字段：

- `sn`: 职业分类编码/职业编码，例如"6-31-01-05"，表示职业的分类层级
- `name`: 职业分类名称/职业名称，例如"锅炉设备检修工"
- `desc`: 职业分类描述/职业描述，包含该职业的主要工作内容、工作任务和可能包含的工种
- `gbmcode`: 职业分类国标码（仅职业分类有此字段，具体职业没有这个字段）

示例数据：

```json
{
  "sn": "6-31-01-05",
  "name": "锅炉设备检修工",
  "desc": "使用工具、量具和仪器、仪表， 维护、检修锅炉本体及辅机、管阀、除灰、除尘、脱硫、脱硝等设备及系统的人员。主要工作任务： 1.准备工器具和设备解体前的装配记录； 2.解体、检查、清理锅炉本体、磨煤机等主辅设备； 3.检测、修复、更换设备零部件； 4.装配锅炉主、辅设备； 5.进行锅炉整体水压试验、辅机试运行， 处理缺陷； 6.检查、验收检修后的设备； 7.采集运行数据， 分析、判断设备状况； 8.填写锅炉检修、试验记录， 编写技术总结报告。本职业包含但不限于下列工种：锅炉本体检修工锅炉管阀检修工锅炉辅机检修工锅炉除灰、脱硫、脱硝设备检修工"
}
```

### 层次化JSON格式 (04_职业分类大典2022_hierarchical.json)

层次化JSON保留了职业分类的嵌套结构，字段含义与扁平化格式相同，但增加了`subclass`字段表示下级分类：

- `sn`: 职业分类编码/职业编码，表示职业的分类层级
- `name`: 职业分类名称/职业名称
- `desc`: 职业分类描述/职业描述
- `gbmcode`: 职业分类国标码（仅职业分类有此字段，具体职业没有这个字段）
- `subclass`: 下级分类数组，包含该分类下的所有子分类或具体职业
- `worktypes`: 包含该职业的具体工种列表（仅部分具体职业有此字段）

示例数据：

```json
{
  "sn": "6-31",
  "name": "生产辅助人员",
  "desc": "从事设备运行、维护和保养等生产辅助工作的人员。",
  "gbmcode": "6310",
  "subclass": [
    {
      "sn": "6-31-01",
      "name": "设备操作人员",
      "desc": "...",
      "gbmcode": "63101",
      "subclass": [
        {
          "sn": "6-31-01-05",
          "name": "锅炉设备检修工",
          "desc": "...",
          "worktypes": [
            "锅炉本体检修工",
            "锅炉管阀检修工",
            "锅炉辅机检修工",
            "锅炉除灰、脱硫、脱硝设备检修工"
          ]
        }
      ]
    }
  ]
}
```

层次化结构的优势在于可以直观地表示职业分类的层级关系，便于构建树状展示界面或进行层级查询。

职业编码(`sn`)的结构说明：
- 第一段数字（如"6"）：表示大类
- 第二段数字（如"31"）：表示中类
- 第三段数字（如"01"）：表示小类
- 第四段数字（如"05"）：表示职业

## 使用方法

您可以通过以下方式使用本数据：

1. 直接下载JSON文件进行本地使用
2. 导入到数据库中进行查询和分析
3. 使用树状索引文件快速浏览职业分类结构
4. 根据需要选择扁平化或层次化的JSON格式

## 数据统计

根据索引文件，本数据集包含：
- 8个大类
- 多个中类、小类和具体职业
- 覆盖了从党政机关、企事业单位负责人到各类专业技术和生产服务人员的全部职业分类

## 贡献指南

欢迎对本项目进行贡献，您可以通过以下方式参与：

- 提交Issue报告数据问题或建议改进方案
- 提交Pull Request完善数据或文档
- 分享本项目，让更多人受益

## 声明

数据收集自网络公开资源，仅用于学习研究。如有侵权问题，请联系我删除。

## 支持项目

如果本项目对您有所帮助，欢迎给我一个Star⭐，这是对我工作的最大鼓励！

## 许可证

本项目是对公开资料的整理工作，原始数据版权归原作者所有。

本项目的JSON数据整理工作采用[MIT许可证](https://opensource.org/licenses/MIT)，允许任何人出于任何目的使用、复制、修改、合并、发布、分发、再许可和/或销售本软件的副本，但须遵守以下条件：

上述版权声明和本许可声明应包含在本软件的所有副本或实质性部分中。

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
