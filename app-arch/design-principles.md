# 应用架构的设计原则

应用架构有比较多的参考设计原则，包括应用设计原则、服务设计原则、服务分层原则、微服务设计原则、接口设计原则、开发设计原则等。在实践过程中，我们可以选择性地加以参考。

## 应用设计原则

应用设计的总体原则可以借鉴第1章中介绍的架构设计原则，即正交性、高内聚、低耦合、简单适用等。此外，在应用设计过程中，还有如下参考。

- **边界清晰**：每个应用的范围和边界要清晰，没有重叠，无重复定义的应用功能，同时应对应合理的组织。
- **拆分和分层**：在满足业务需求的情况下，多考虑应用和系统如何拆分和分层，控制粒度，将核心、稳定、可复用的业务能力进行抽象和沉淀。
- **线性扩展**：企业需要采用去中心化架构，服务尽量无状态，便于水平扩展。在设计时，还需要考虑应用和服务的扩展能力，如流程扩展、服务扩展、编排扩展、界面配置，以及开放能力和对外集成能力等。
- **数据化运营**：应用功能内部数据共享最大化，应用功能之间共享最小化。通过运营指标驱动，增强数字化运维、监控告警、限流降级、性能分析和诊断等方面的能力。
- **异步化**：互联网应用一般不苛求强一致性，而使用最终一致来平衡。在业务允许范围内，尽可能采用异步解耦，比如不同域之间异步调用，核心业务异步调用非核心业务，而同步调用的，需设置超时时间及重试机制等。
- **自动化管控**：提升自动化运维能力，如自动部署、自动弹性扩容、自动升降级、自动限流降级等，降低运营成本，提高系统的稳定性和业务连续性。

## 服务设计原则

应用架构是以服务为中心的，在进行服务设计时需要遵循以下原则。

- **稳定性原则**：一切以系统稳定为核心，不允许过度设计，应用架构应尽可能清晰、简单。
- **松耦合原则**：各个应用确保稳定部分与易变部分，核心业务与非核心业务、服务提供者与服务消费者、核心服务与非核心服务、应用与数据、服务与实现细节等分离。
- **抽象化原则**：确保应用抽象化、数据存储抽象化、服务计算抽象化。
- **容错原则**：通过自治、冗余、延缓等手段提高服务的容错能力，通过服务自治、服务隔离、限流降级等避免出现连锁反应，通过集群容错、避免单点、服务中心容灾等提高系统容错能力。
- **安全性原则**：采用多层安全防火设计，提高系统的故障恢复、应急响应能力，阻止来自外部的非法访问，预防黑客攻击，服务数据等安全合规，系统应具备数据备份和恢复能力等。
- **规范统一原则**：通过统一接口方式和管控手段，统一规划建设、统一标准管理，信息共享，协同合作。
- **开放扩展原则**：服务的数据交换符合行业标准，提供服务的扩展能力，包括服务流程、服务接口、应用等多层次定制化扩展能力。
- **服务无状态原则**：服务设计为可以伸缩的，并且可以部署到高可用性基础结构中，尽可能减少服务的状态，或者通过分布式存储方式来保存。

## 服务分层原则

服务分层对于服务设计非常重要。对服务进行分层后可以使我们讨论问题聚焦在某一层上，降低问题的复杂度。一些服务分层原则如下。

- **高内聚、低耦合**：服务分层的首要原则是高内聚、低耦合，即服务内部高度内聚，服务外部降低耦合度。在分层时，我们可以每次从不同的角度进行，通过多次优化，减少服务与服务之间的依赖。
- **基于通用性进行分层**：稳定、通用的服务向下沉淀，个性、定制化的服务向上沉淀，同时可以设计一些变化的分层来隔离变化。另外，还有其他考虑维度，如是否是非功能性服务、是否是平台类型服务、是否是重要服务等。
- **团队规模参考**：以垂直业务划分开发维护团队，澄清跨团队服务消费需求，并订立服务契约，3～8人的开发维护团队为理想规模。同时，需要架构委员会处理跨域冲突，处理有冲突的服务能力归属等跨组织的协调问题。
- **数据访问原则**：数据归属应该单一化，跨域数据读写需要尽量减少，并且严格遵循依赖原则及接口访问原则。
- **服务依赖原则**：服务分层访问，上层可调用同层或下层服务，禁止下层调用上层服务，同时要对跨层访问次数加以限制，为后续限流降级打好基础。
- **共享服务划分原则**：是否足够通用、普适，是否高度抽象，可以被不同业务进行定制和扩展；是否有业务价值，可以解决某种通用的业务问题；是否有业务数据的持续输入，架构运营的核心是数据，如果一个服务数据输入不足，则可以先不考虑共享；是否能力相对稳定，共享服务会迭代变化，但不应该变化过于频繁。

## 微服务设计原则

这里从应用服务设计角度介绍一些微服务设计原则。

- **业务优先原则**：当有冲突时，以业务需求为核心。
- **顶层架构设计原则**：以业务架构为设计基础，遵循顶层业务架构的设计。
- **稳定性原则**：以稳定为中心，设计得尽可能简单和清晰，不过度设计。
- **依赖和分离原则**：需要把稳定的服务部分与易变的服务部分进行分离，把核心业务微服务与非核心业务微服务分离，应用与数据分离，服务接口与实现细节分离。
- **异步松耦合原则**：不同业务域间尽量异步解耦；核心业务与非核心业务间尽量异步解耦。
- **垂直划分优先原则**：尽可能根据业务领域进行服务的垂直划分，这样更加关注业务实现，端到端负责，便于持续改进，减少调用次数。水平划分需要充分从总体考虑。
- **持续演进原则**：应逐步划分、持续演进，避免服务数量的“爆炸性”增长。当服务数量增加时，需要考虑持续交付、微服务监控与治理等环节。
- **服务自治原则**：服务需要提供SLA，保持稳定性，可以独立开发、测试、部署和运行，避免发生连锁反应。
- **自动化驱动原则**：可以结合DevOps和CI/CD等自动化工具，以及成熟的微服务治理框架，提高微服务生命周期的自动化效率。
- **微服务拆分原则**：优先拆分比较独立的服务、通用服务、边界明显的服务、核心服务。

## 接口设计原则

服务之间交流的契约是API，一个好的接口应该是无状态、标准且兼容的，技术上目前采用比较多的是RESTful API。下面介绍一些通用的接口设计原则。

- **合适粒度原则**：平衡可维护性与易用性。可提供普适的粗粒度业务逻辑片段，根据需求增加精细化的服务接口。
- **强描述性原则**：服务名和方法的意义明确，表意精准，服务模式明确，比如是同步还是异步。
- **内聚完整原则**：从服务消费者的角度，考察提供服务的完整性、功能的自洽性。
- **语义接口原则**：接口信息使用语义化封装，内外隔离，接口信息对象独立于服务内部的实现信息对象定义。
- **接口普适原则**：接口信息基本属性尽量使用跨语言的基本类型（字符串、日期、数值等）。
- **扩展兼容原则**：在保证易用性的前提下，尽可能考虑扩展性，避免未来频繁更改接口，同时做好版本管理。
- **服务命名原则**：自描述，易于理解，并且有意义。
- **契约先行原则**：当与其他团队交流时，双方的交流基础就是接口，要形成契约意识，对双方形成强有力的约束，并为双方提供保障。

## 开发设计原则

在开发过程中，一些关于设计阶段的通用参考如下所示。

- **定义相关的技术规范**：包括服务设计规范、接口设计规范、Java开发规范、产品使用规范、数据库使用规范、部署升级规范、运维规范、编程规范、日志规范、工程规范、安全规范等。
- **应用开发原则**：边界清晰、应用内数据共享；应用间依赖最小化，不存在循环依赖；应用可管理、可监控、可开发、可扩展。
- **服务开发规范**：考虑如下设计，如超时重试、快速失败、结果可预期、服务无状态、幂等性、乱序可容忍、无循环依赖。
