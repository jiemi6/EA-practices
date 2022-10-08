# 数据架构参考实践

## 通用数据架构

这里给出一个通用的数据架构以供参考，如图6-6所示，通过分层的视角列出了一些相对核心的层次，每个层次的内容并不固定，我们需要根据具体的业务和数据需求进行调整。

![通用数据架构](images/General-data-architecture.png)

> 图例：通用数据架构

- **数据服务**：**构建数据服务层，通过接口服务化方式对外提供数据服务**。比如对应的数据目录、数据标签、数据分析、算法模型（如智能补货算法、信用风险模型、商品推荐模型、客户留存模型、转化漏斗算法），并结合相应的数据应用、数据产品和分析模型，**提供对应的公共数据服务能力**。
- **数据计算**：**数据只有被整合、计算才能被用于洞察规律、挖掘潜在信息，实现数据价值**，可以包括批量离线、内存计算、在线流式、机器学习等。
- **数据存储**：**支撑数据的数据库及存储技术**，包括关系型、NoSQL、分析型、其他存储方式，具体的分类和选型可以参考本章相关内容。
- **数据采集**：一套**标准的数据采集体系**，包括结构化、非结构化、半结构化数据的采集，还要做好数据传输。
- **工具平台**：需要搭建一些工具或平台，
  - 智能研发平台（从数据开发流程上辅助开发人员进行数据研发，如构建数据模型、算法开发、数据服务等）
  - 智能分析平台（针对数据进行灵活、快速的分析，支持多数据源、多维分析、多图表组件、多用户权限、多屏等）
  - 智能标签平台（进行标签的定义、可视化及相应的管理）
  - 智能运维平台（对工具平台的服务组件及集群节点的健康状态进行监控）
  - 大数据分析平台（构建大数据处理分析能力，包括相应的组件）

## 结合应用架构

在应用架构中，我们介绍了一些[基于DDD的通用应用中心](../app-arch/domain-driven-design.md)，核心是对应的领域模型。在数据架构中，可以很好地承接这些领域模型到数据模型，并逐步形成相应的数据和存储规划。

> 这里需要强调的是，**领域模型和数据模型并不一定是一对一的关系，前者面向DDD的领域实体，后者面向数据规划层面**，比如一个会员积分领域模型，可能对应数据库中的会员积分表、积分明细表、积分快照等多张表。

这个过程也需要结合数据架构设计方法和步骤，对整体数据进行分析，这里推荐结合应用架构进行数据架构。

![结合应用架构进行数据架构](images/Data-architecture-combined-with-application-architecture.png)

> 图例：结合应用架构进行数据架构

- **数据规划**：总体规划，根据企业战略计划、业务架构和应用架构相应输入（如业务流程和应用场景），明确需要建设的数据主题域、相关的资源配置、技术选型等。
- **数据采集**：对接相应的数据源，根据对应数据进行基础的采集、清洗和结构化处理。
- **数据建模**：明确对应的主题，同时确定相应的聚合粒度、对应的数据指标、总体规范定义等。
- **数据萃取**：根据数据进行萃取管理，识别统一ID，建立标签画像，进行相应数据服务的开发。
- **数据资产管理**：整合数据服务能力，构建数据地图，并结合资产应用和指标管理体系，沉淀数据模型等关键数据资产。
- **数据治理**：将数据服务进一步标准化、可视化，并经过多维分析和运维治理，对数据的生命周期进行治理。