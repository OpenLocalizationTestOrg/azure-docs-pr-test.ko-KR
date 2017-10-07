---
title: "aaaSCP.NET 프로그래밍 가이드 | Microsoft Docs"
description: "자세한 내용은 방법 toouse SCP.NET toocreate 합니다. 에 대 한.NET 기반 스톰 토폴로지 HDInsight의 Storm를 사용 합니다."
services: hdinsight
documentationcenter: 
author: raviperi
manager: jhubbard
editor: cgronlun
ms.assetid: 34192ed0-b1d1-4cf7-a3d4-5466301cf307
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/16/2016
ms.author: raviperi
ms.openlocfilehash: a57f4217b07e0e82a3f36650308695fbb45d9128
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="scp-programming-guide"></a>SCP 프로그래밍 가이드
SCP은 플랫폼 toobuild 실시간으로, 신뢰할 수 있는 일관 되 고 높은 성능 데이터 처리 응용 프로그램입니다. 맨 위에 구축 [Apache Storm](http://storm.incubator.apache.org/) -스트림 hello OSS 커뮤니티도 설계 된 시스템을 처리 합니다. Nathan Marz가 디자인한 Storm은 Twitter에서 오픈 소스 방식으로 제공되며, 활용 [Apache 사육](http://zookeeper.apache.org/), 다른 Apache 프로젝트 tooenable 매우 안정적 분산된 조정 및 상태 관리 합니다. 

Hello SCP 프로젝트 포팅 Windows에서 Storm 할 뿐만 아니라 hello 프로젝트 확장명 및 사용자 지정 hello Windows 환경에도 추가 합니다. .NET 개발자 환경 및 라이브러리를 포함 하는 hello 확장, hello 사용자 지정 Windows 기반 배포를 포함 합니다. 

toofork hello OSS 프로젝트 필요 하지 않습니다 및 파생된 에코 시스템 Storm 기반으로 활용 하 여 수 hello 확장 및 사용자 지정 방식으로 수행 됩니다.

## <a name="processing-model"></a>처리 모델
SCP의 hello 데이터 튜플 스트림을 지속적으로 모델링 됩니다. 일반적으로 hello 튜플 대기열으로 이동 일부 먼저 다음을 선택 하 고 스톰 토폴로지 내에서 호스팅되는 비즈니스 논리에 의해 변환, 마지막으로 hello 출력 튜플 tooanother SCP 시스템으로 파이프 될 수 없습니다 이나 커밋된 toostores 수 같은 분산된 파일 시스템 또는 데이터베이스 같은 SQL Server입니다.

![피드는 데이터 저장소는 데이터 tooprocessing을 제공 하는 큐의 다이어그램](media/hdinsight-storm-scp-programming-guide/queue-feeding-data-to-processing-to-data-store.png)

Storm에서는 응용 프로그램 토폴로지에 따라 계산 그래프가 정의됩니다. 토폴로지의 각 노드에는 처리 논리가 포함되며 노드 간의 링크는 데이터 흐름을 나타냅니다. hello 노드 tooinject 입력된 데이터를 hello 토폴로지 Spouts 사용된 toosequence hello 데이터 될 수 있는 호출 됩니다. hello 입력된 데이터 수에 있는 로그 파일, 트랜잭션 데이터베이스, 시스템 성능 카운터 두 입력 및 출력 데이터 흐름이 사용 하는 등 hello 노드가 볼트 실제 데이터 필터링 hello 수행 하 고 선택 항목 및 집계 라고 합니다.

SCP는 최상의 노력, 최소한 한 번 및 정확히 한 번 방식의 데이터 처리를 지원합니다. 분산된 스트리밍 처리 응용 프로그램에서 네트워크 중단, 컴퓨터 오류 또는 사용자 코드 오류 등과 같은 데이터 처리 중 다양한 오류가 발생할 수 있습니다. 최소-한 번에 처리 되도록 모든 데이터를 처리할지 적어도 한 번 자동으로 다시 재생 하 여 동일한 데이터 오류가 발생 하는 경우 hello 합니다. 최소한 한 번 방식의 처리는 간단하고 안정적이며 대부분의 응용 프로그램에 적합합니다. 그러나 hello 응용 프로그램이 정확한 계산을 요구 하는 경우 예를 들어 최소-한 번에 처리 충분 하지 않습니다 hello 동일한 데이터 수 잠재적으로 재생할 수 hello 응용 프로그램 토폴로지에 있으므로. 이 경우, 정확 하 게-hello 데이터를 재생 하 고 여러 번 처리 될 수 있습니다 하는 경우에 toomake 있는지 hello 결과 올바른 일단 처리 설계 되었습니다.

SCP 활용 hello 가상 컴퓨터 JVM (Java) hello 커버에서 Storm 기반 하는 동안.NET 개발자 toodevelop 실시간으로 데이터 프로세스 응용 프로그램을 사용 합니다. hello.NET 및 JVM 로컬 TCP 소켓을 통해 통신합니다. 기본적으로 각 배출구/볼트 hello 사용자 논리.Net 플러그 인 프로세스에서 실행 되는.Net/Java 프로세스 쌍입니다.

toobuild 처리 SCP 기반으로 응용 프로그램 데이터를 여러 단계가 필요 합니다.

* 디자인 하 고 큐에서 데이터의 hello Spouts toopull를 구현 합니다.
* 디자인 및 볼트 tooprocess hello 입력된 데이터를 구현 하 고 데이터베이스 같은 tooexternal 저장소에 데이터를 저장 합니다.
* Hello 토폴로지를 디자인, 전송 및 hello 토폴로지를 실행 합니다. hello 토폴로지 정의 정점 및 hello 데이터 hello 꼭지점 사이의 흐름. SCP은 hello 토폴로지 사양 걸리고 Storm 클러스터를 각 꼭 짓 논리 노드 하나에서 실행 되는 위치에 배포 됩니다. hello 장애 조치 및 크기 조정 됩니다 처리 hello 스톰 작업 스케줄러입니다.

이 문서는 방법을 통해 몇 가지 간단한 예 toowalk ´ ֲ SCP toobuild 데이터 처리 응용 프로그램입니다.

## <a name="scp-plugin-interface"></a>SCP 플러그 인 인터페이스
SCP 플러그 인 (또는 응용 프로그램)는 독립 실행형 Exe 실행할 수 있는 둘 다 Visual Studio 내 hello 개발 단계에서는 프로덕션 환경에서 배포 후 hello 스톰 파이프라인에 연결 합니다. Hello SCP 플러그 인을 작성 다른 표준 Windows 콘솔 응용 프로그램 작성 동일 방금 hello 됩니다. SCP.NET 플랫폼 배출구/모양에 대 한 몇 가지 인터페이스를 선언 하 고 hello 사용자 플러그 인 코드는 이러한 인터페이스를 구현 해야 합니다. 이 디자인의 주요 목적은 hello은 해당 hello 사용자는 자신의 비즈니스 logics 고 SCP.NET 플랫폼에서 처리 하는 다른 작업 toobe에 집중할 수 있습니다.

hello 사용자 플러그 인 코드 hello 다음 인터페이스 중 하나를 구현 해야, hello 토폴로지 트랜잭션 또는 비트랜잭션 인지와 배출구 인지 볼트 hello 구성 요소 인지에 따라 달라 집니다.

* ISCPSpout
* ISCPBolt
* ISCPTxSpout
* ISCPBatchBolt

### <a name="iscpplugin"></a>ISCPPlugin
ISCPPlugin는 모든 종류의 플러그 인에 대 한 hello 공용 인터페이스입니다. 현재는 더미 인터페이스입니다.

    public interface ISCPPlugin 
    {
    }

### <a name="iscpspout"></a>ISCPSpout
ISCPSpout는 hello 인터페이스 비트랜잭션 배출구입니다.

     public interface ISCPSpout : ISCPPlugin                    
     {
         void NextTuple(Dictionary<string, Object> parms);         
         void Ack(long seqId, Dictionary<string, Object> parms);   
         void Fail(long seqId, Dictionary<string, Object> parms);  
     }

때 `NextTuple()` 호출 hello C\# 사용자 코드에서 하나 이상의 튜플과 내보낼 수 있습니다. 내용이 없는 경우 tooemit,이 메서드는 아무 것도 표시 하지 않고 반환 합니다. `NextTuple()`, `Ack()` 및 `Fail()`은 모두 C\# 프로세스 내 단일 스레드의 조밀한 루프에서 호출됩니다. 없는 튜플 tooemit 인 경우 courteous toohave NextTuple 절전 짧은 시간 (예: 10 밀리초)으로 toowaste 하지 않으므로 CPU를 너무 많이 있습니다.

`Ack()` 및 `Fail()`은(는) 사양 파일에서 승인 메커니즘이 사용하도록 설정되어 있어야 호출됩니다. hello `seqId` 했지만 했는지 아니면 실패 했는지를 사용 하는 tooidentify hello 튜플 됩니다. 따라서 ack 비트랜잭션 토폴로지에서 활성화 된 경우 emit 함수 다음 hello 배출구에 사용 되어야 합니다.

    public abstract void Emit(string streamId, List<object> values, long seqId); 

Ack 비트랜잭션 토폴로지에서 지원 되지 않는 경우 hello `Ack()` 및 `Fail()` 빈 함수로 유지할 수 있습니다.

hello `parms` 이러한 함수에 입력된 매개 변수는 똑같이 비어 있는 사전, 나중에 사용 하도록 예약 합니다.

### <a name="iscpbolt"></a>ISCPBolt
ISCPBolt는 hello 인터페이스 비트랜잭션 볼트입니다.

    public interface ISCPBolt : ISCPPlugin 
    {
    void Execute(SCPTuple tuple);           
    }

새 튜플을 사용할 수 있는 hello `Execute()` 함수를 호출할지 tooprocess 것입니다.

### <a name="iscptxspout"></a>ISCPTxSpout
ISCPTxSpout는 hello 인터페이스 트랜잭션 배출구입니다.

    public interface ISCPTxSpout : ISCPPlugin
    {
        void NextTx(out long seqId, Dictionary<string, Object> parms);  
        void Ack(long seqId, Dictionary<string, Object> parms);         
        void Fail(long seqId, Dictionary<string, Object> parms);        
    }

해당하는 비트랜잭션 함수와 마찬가지로 `NextTx()`, `Ack()` 및 `Fail()`은 모두 C\# 프로세스 내 단일 스레드의 조밀한 루프에서 호출됩니다. 없는 데이터 tooemit 인 경우에 courteous toohave `NextTx` 절전 모드는 짧은 시간 (10 밀리초) 동안 따라서 하지 toowaste로 CPU를 너무 많이 있습니다.

`NextTx()`위에 호출 되는 새 트랜잭션을 toostart hello 매개 변수 `seqId` 에 사용 되는 사용 되는 tooidentify hello 트랜잭션이 `Ack()` 및 `Fail()`합니다. `NextTx()`, 사용자 데이터 tooJava 측면을 내보낼 수 있습니다. hello 데이터 사육 toosupport 재생에 저장 됩니다. Hello 용량의 사육 매우 제한적 이기 때문에 사용자만 메타 데이터를 트랜잭션 배출구에 데이터를 대량 내보내야 합니다.

Storm에서는 트랜잭션이 실패하면 자동으로 재생하므로 일반적인 경우에는 `Fail()` 을(를) 호출하면 안 됩니다. SCP 트랜잭션 배출구에서 내보내는 hello 메타 데이터를 확인할 수를 호출할 수 있습니다 하지만 `Fail()` hello 메타 데이터가 유효 하지 않은 경우.

hello `parms` 이러한 함수에 입력된 매개 변수는 똑같이 비어 있는 사전, 나중에 사용 하도록 예약 합니다.

### <a name="iscpbatchbolt"></a>ISCPBatchBolt
ISCPBatchBolt는 트랜잭션 모양에 대 한 hello 인터페이스입니다.

    public interface ISCPBatchBolt : ISCPPlugin           
    {
        void Execute(SCPTuple tuple);
        void FinishBatch(Dictionary<string, Object> parms);  
    }

`Execute()`새 튜플 hello 볼트에 도착 하는 경우 호출 됩니다. `FinishBatch()` 이(가) 호출됩니다. hello `parms` 입력된 매개 변수는 사용 하도록 예약 합니다.

트랜잭션 토폴로지에는 `StormTxAttempt`(이)라는 중요한 개념이 있습니다. 두 필드 `TxId` 및 `AttemptId`가 있습니다. `TxId`tooidentify 사용 되는 특정 트랜잭션에 이며 지정된 된 트랜잭션이 있을 수 여러 시도 hello 트랜잭션이 실패 하 고는 재생 합니다. SCP.NET 됩니다는 다른 ISCPBatchBolt 개체 tooprocess 각 새로운 `StormTxAttempt`마찬가지로 Java 쪽에서 어떤 스톰 수행 합니다. hello이이 디자인의 목적은 toosupport 병렬 트랜잭션을 처리 합니다. 사용자에에서 보관 해야 유의 해야 하는 트랜잭션 시도가 완료 된 hello 해당 ISCPBatchBolt 개체가 소멸 됩니다 하 고 가비지 수집 합니다.

## <a name="object-model"></a>개체 모델
또한 SCP.NET와 개발자가 tooprogram 키 개체의 간단한 집합을 제공합니다. 이러한 개체는 **Context**, **StateStore** 및 **SCPRuntime**입니다. 이 섹션의 hello 나머지 부분에서 설명 합니다.

### <a name="context"></a>Context
컨텍스트는 실행 중인 환경 toohello 응용 프로그램을 제공합니다. 각 ISCPPlugin 인스턴스(ISCPSpout/ISCPBolt/ISCPTxSpout/ISCPBatchBolt)에는 해당하는 Context 인스턴스가 있습니다. 상황에 맞는에서 제공 하는 hello 기능 두 부분으로 나눌 수 있습니다: (1) hello 정적 부분에서 사용할 수 있는 전체 C hello\# 에서만 hello 특정 컨텍스트 인스턴스에 대해 사용할 수 있는 (2) hello 동적 부분을 처리 합니다.

### <a name="static-part"></a>정적 부분
    public static ILogger Logger = null;
    public static SCPPluginType pluginType;                      
    public static Config Config { get; set; }                    
    public static TopologyContext TopologyContext { get; set; }  

`Logger` 은(는) 기록용으로 제공됩니다.

`pluginType`가 사용 되는 C hello 유형의 hello 플러그 인 tooindicate\# 프로세스입니다. 경우 hello C\# (Java) 없이 로컬 테스트 모드에서 프로세스를 실행 하는 hello 플러그 인 형식은, `SCP_NET_LOCAL`합니다.

    public enum SCPPluginType 
    {
        SCP_NET_LOCAL = 0,       
        SCP_NET_SPOUT = 1,       
        SCP_NET_BOLT = 2,        
        SCP_NET_TX_SPOUT = 3,   
        SCP_NET_BATCH_BOLT = 4  
    }

`Config`Java 쪽에서 tooget 구성 매개 변수를 제공 됩니다. hello 매개 변수는 Java 로부터 전달 때 C\# 플러그 인 초기화 됩니다. hello `Config` 매개 변수는 두 부분으로 나뉘어: `stormConf` 및 `pluginConf`합니다.

    public Dictionary<string, Object> stormConf { get; set; }  
    public Dictionary<string, Object> pluginConf { get; set; }  

`stormConf`가 정의 된 매개 변수는 및 `pluginConf` SCP에 정의 된 hello 매개 변수는 합니다. 예:

    public class Constants
    {
        … …

        // constant string for pluginConf
        public static readonly String NONTRANSACTIONAL_ENABLE_ACK = "nontransactional.ack.enabled";  

        // constant string for stormConf
        public static readonly String STORM_ZOOKEEPER_SERVERS = "storm.zookeeper.servers";           
        public static readonly String STORM_ZOOKEEPER_PORT = "storm.zookeeper.port";                 
    }

`TopologyContext`여러 병렬 처리 수준 구성 요소에 대 한 가장 유용 tooget hello 토폴로지 컨텍스트 제공 됩니다. 다음은 예제입니다.

    //demo how tooget TopologyContext info
    if (Context.pluginType != SCPPluginType.SCP_NET_LOCAL)                      
    {
        Context.Logger.Info("TopologyContext info:");
        TopologyContext topologyContext = Context.TopologyContext;                    
        Context.Logger.Info("taskId: {0}", topologyContext.GetThisTaskId());          
        taskIndex = topologyContext.GetThisTaskIndex();
        Context.Logger.Info("taskIndex: {0}", taskIndex);
        string componentId = topologyContext.GetThisComponentId();                    
        Context.Logger.Info("componentId: {0}", componentId);
        List<int> componentTasks = topologyContext.GetComponentTasks(componentId);  
        Context.Logger.Info("taskNum: {0}", componentTasks.Count);                    
    }

### <a name="dynamic-part"></a>동적 부분
인터페이스 다음 hello 관련 tooa 특정 컨텍스트 인스턴스가 됩니다. hello 컨텍스트 인스턴스가 SCP.NET 플랫폼에서 만들고 toohello 사용자 코드를 전달 합니다.

    // Declare hello Output and Input Stream Schemas

    public void DeclareComponentSchema(ComponentStreamSchema schema);   

    // Emit tuple toodefault stream.
    public abstract void Emit(List<object> values);                   

    // Emit tuple toohello specific stream.
    public abstract void Emit(string streamId, List<object> values);  

Ack를 지 원하는 비트랜잭션 배출구에 대 한 메서드를 다음 hello 제공 됩니다.

    // for non-transactional Spout which supports ack
    public abstract void Emit(string streamId, List<object> values, long seqId);  

Ack를 지 원하는 비트랜잭션 볼트에 대 한 기본 프린터를 사용할지 명시적으로 `Ack()` 또는 `Fail()` hello 튜플 개 수신 합니다. 및 새 튜플을 내보낼 때 hello 새 튜플의 hello 앵커 지정 해야 합니다. 메서드를 다음 hello 제공 됩니다.

    public abstract void Emit(string streamId, IEnumerable<SCPTuple> anchors, List<object> values); 
    public abstract void Ack(SCPTuple tuple);
    public abstract void Fail(SCPTuple tuple);

### <a name="statestore"></a>StateStore
`StateStore` 은(는) 메타데이터 서비스, 단조 시퀀스 생성 및 비대기 조정 기능을 제공합니다. `StateStore`을(를) 기반으로 하여 분산 잠금, 분산 큐, 장벽 및 트랜잭션 서비스를 비롯한 높은 수준의 분산형 동시성 추상화를 작성할 수 있습니다.

SCP 응용 프로그램 수 hello를 사용 하 여 `State` toopersist 트랜잭션 토폴로지를 위해 특별히 사육의 일부 정보 개체입니다. 충돌 하 고 다시 시작 하는 트랜잭션 배출구, 사육에서 hello 필요한 정보를 검색 하 고 hello 파이프라인 다시 시작 수 있도록 수행 합니다.

hello `StateStore` 개체에는 이러한 메서드가 주로:

    /// <summary>
    /// Static method tooretrieve a state store of hello given path and connStr 
    /// </summary>
    /// <param name="storePath">StateStore Path</param>
    /// <param name="connStr">StateStore Address</param>
    /// <returns>Instance of StateStore</returns>
    public static StateStore Get(string storePath, string connStr);

    /// <summary>
    /// Create a new state object in this state store instance
    /// </summary>
    /// <returns>State from StateStore</returns>
    public State Create();

    /// <summary>
    /// Retrieve all states that were previously uncommitted, excluding all aborted states 
    /// </summary>
    /// <returns>Uncommited States</returns>
    public IEnumerable<State> GetUnCommitted();

    /// <summary>
    /// Get all hello States in hello StateStore
    /// </summary>
    /// <returns>All hello States</returns>
    public IEnumerable<State> States();

    /// <summary>
    /// Get state or registry object
    /// </summary>
    /// <param name="info">Registry Name(Registry only)</param>
    /// <typeparam name="T">Type, Registry or State</typeparam>
    /// <returns>Return Registry or State</returns>
    public T Get<T>(string info = null);

    /// <summary>
    /// List all hello committed states
    /// </summary>
    /// <returns>Registries contain hello Committed State </returns> 
    public IEnumerable<Registry> Commited();

    /// <summary>
    /// List all hello Aborted State in hello StateStore
    /// </summary>
    /// <returns>Registries contain hello Aborted State</returns>
    public IEnumerable<Registry> Aborted();

    /// <summary>
    /// Retrieve an existing state object from this state store instance 
    /// </summary>
    /// <returns>State from StateStore</returns>
    /// <typeparam name="T">stateId, id of hello State</typeparam>
    public State GetState(long stateId)

hello `State` 개체에는 이러한 메서드가 주로:

    /// <summary>
    /// Set hello status of hello state object toocommit 
    /// </summary>
    public void Commit(bool simpleMode = true); 

    /// <summary>
    /// Set hello status of hello state object tooabort 
    /// </summary>
    public void Abort();

    /// <summary>
    /// Put an attribute value under hello give key 
    /// </summary>
    /// <param name="key">Key</param> 
    /// <param name="attribute">State Attribute</param> 
    public void PutAttribute<T>(string key, T attribute); 

    /// <summary>
    /// Get hello attribute value associated with hello given key 
    /// </summary>
    /// <param name="key">Key</param> 
    /// <returns>State Attribute</returns>               
    public T GetAttribute<T>(string key);                    

Hello에 대 한 `Commit()` 메서드 simpleMode tootrue 설정 된 경우, 단순히 삭제 됩니다 hello ZNode 사육에 해당 합니다. 그렇지 않으면 삭제 됩니다 커밋됨 hello에 새 노드를 추가 하 고 현재 ZNode hello\_경로입니다.

### <a name="scpruntime"></a>SCPRuntime
SCPRuntime hello 다음 두 가지 방법을 제공 합니다.

    public static void Initialize();

    public static void LaunchPlugin(newSCPPlugin createDelegate);  

`Initialize()`사용 되는 tooinitialize hello SCP 런타임 환경이입니다. 이 방법에서는 C hello\# 프로세스 toohello Java 쪽 및 가져옵니다 구성 매개 변수 및 토폴로지 컨텍스트 연결 됩니다.

`LaunchPlugin()`사용 되는 tookick hello 메시지 처리 루프 있습니다. 이 루프에서 C hello\# hello 메시지 처리, hello 인터페이스 메서드를 호출 하는 아마도 hello 사용자 코드에 의해 제공 되는 다음와 플러그 인에는 메시지 양식 Java 쪽 (튜플 및 제어 신호 포함)를 받습니다. 메서드에 대 한 입력된 매개 변수 hello `LaunchPlugin()` ISCPSpout/IScpBolt/ISCPTxSpout/ISCPBatchBolt 인터페이스를 구현 하는 개체를 반환할 수 있는 대리자입니다.

    public delegate ISCPPlugin newSCPPlugin(Context ctx, Dictionary\<string, Object\> parms); 

얻을 수 ISCPBatchBolt에 대 한 `StormTxAttempt` 에서 `parms`, 재생된 시도 인지 toojudge을 사용 합니다. 이 일반적으로 hello 커밋 볼트에서 수행 되 고 hello에 설명 된 `HelloWorldTx` 예제입니다.

일반적으로 여기에 두 가지 모드 hello SCP 플러그 인 실행 될 수 있습니다.

1. 로컬 테스트 모드:이 모드에서는 hello SCP 플러그 인 (C hello\# 사용자 코드) hello 개발 단계 중에 Visual Studio 내에서 실행 합니다. `LocalContext`메서드 tooserialize 내보내는 hello 튜플 toolocal 파일 및 toomemory 다시 읽기를 제공 하는이 모드에서 사용할 수 있습니다.
   
        public interface ILocalContext
        {
            List\<SCPTuple\> RecvFromMsgQueue();
            void WriteMsgQueueToFile(string filepath, bool append = false);  
            void ReadFromFileToMsgQueue(string filepath);                    
        }
2. 일반 모드:이 모드에서 SCP 플러그 인 hello 스톰 java 프로세스에 의해 시작 됩니다.
   
    SCP 플러그 인을 시작하는 예는 다음과 같습니다.
   
        namespace Scp.App.HelloWorld
        {
        public class Generator : ISCPSpout
        {
            … …
            public static Generator Get(Context ctx, Dictionary<string, Object> parms)
            {
            return new Generator(ctx);
            }
        }
   
        class HelloWorld
        {
            static void Main(string[] args)
            {
            /* Setting hello environment variable here can change hello log file name */
            System.Environment.SetEnvironmentVariable("microsoft.scp.logPrefix", "HelloWorld");
   
            SCPRuntime.Initialize();
            SCPRuntime.LaunchPlugin(new newSCPPlugin(Generator.Get));
            }
        }
        }

## <a name="topology-specification-language"></a>토폴로지 사양 언어
SCP 토폴로지 사양은 SCP 토폴로지를 설명하고 구성하기 위한 도메인별 언어로, Storm의 Clojure DSL(<http://storm.incubator.apache.org/documentation/Clojure-DSL.html>)을 기반으로 하며 SCP에 의해 확장됩니다.

토폴로지 사양 toostorm hello를 통해 실행에 대 한 클러스터 직접 전송할 수 ***runspec*** 명령입니다.

SCP.NET 수행 함수 toodefine hello 트랜잭션 토폴로지를 추가 했습니다.

| **새 함수** | **매개 변수** | **설명** |
| --- | --- | --- |
| **tx-topolopy** |topology-name<br />spout-map<br />bolt-map |Hello 토폴로지 이름의 트랜잭션 토폴로지 정의 &nbsp;정의 맵과 hello 볼트 정의 맵이 spouts |
| **scp-tx-spout** |exec-name<br />args<br />fields |트랜잭션 Spout를 정의합니다. Hello 응용 프로그램을 실행 ***exec 이름*** 를 사용 하 여 ***args***합니다.<br /><br />hello ***필드*** 배출구에 대 한 hello 출력 필드는 |
| **scp-tx-batch-bolt** |exec-name<br />args<br />fields |트랜잭션 Batch Bolt를 정의합니다. Hello 응용 프로그램을 실행 ***exec 이름*** 를 사용 하 여 ***args입니다.***<br /><br />hello 필드는 hello 출력 필드에 대 한 모양입니다. |
| **scp-tx-commit-bolt** |exec-name<br />args<br />fields |트랜잭션 Committer Bolt를 정의합니다. Hello 응용 프로그램을 실행 ***exec 이름*** 를 사용 하 여 ***args***합니다.<br /><br />hello ***필드*** 모양에 대 한 hello 출력 필드는 |
| **nontx-topolopy** |topology-name<br />spout-map<br />bolt-map |Hello 토폴로지 이름의 비트랜잭션 토폴로지 정의&nbsp; 정의 맵과 hello 볼트 정의 맵이 spouts |
| **scp-spout** |exec-name<br />args<br />fields<br />매개 변수 |비트랜잭션 Spout를 정의합니다. Hello 응용 프로그램을 실행 ***exec 이름*** 를 사용 하 여 ***args***합니다.<br /><br />hello ***필드*** 배출구에 대 한 hello 출력 필드는<br /><br />hello ***매개 변수*** 선택적 toospecify 사용 하는 "nontransactional.ack.enabled" 등의 일부 매개 변수입니다. |
| **scp-bolt** |exec-name<br />args<br />fields<br />매개 변수 |비트랜잭션 Bolt를 정의합니다. Hello 응용 프로그램을 실행 ***exec 이름*** 를 사용 하 여 ***args***합니다.<br /><br />hello ***필드*** 모양에 대 한 hello 출력 필드는<br /><br />hello ***매개 변수*** 선택적 toospecify 사용 하는 "nontransactional.ack.enabled" 등의 일부 매개 변수입니다. |

SCP.NET에서는 다음 키워드가 정의됩니다.

| **키워드** | **설명** |
| --- | --- |
| **:name** |Hello 토폴로지 이름 정의 |
| **:topology** |정의 함수에 위에 hello를 사용 하 여 토폴로지를 hello 및 스토리에서 작성 합니다. |
| **:p** |각 배출구 또는 번개 hello 병렬 처리 수준 힌트를 정의 합니다. |
| **:config** |정의 업데이트 기존 hello 또는 매개 변수 구성 |
| **:schema** |Hello 스트림 스키마를 정의 합니다. |

그 외에 자주 사용되는 매개 변수는 다음과 같습니다.

| **매개 변수** | **설명** |
| --- | --- |
| **"plugin.name"** |hello C# 플러그 인의 exe 파일 이름 |
| **"plugin.args"** |플러그 인 인수입니다. |
| **"output.schema"** |출력 스키마입니다. |
| **"nontransactional.ack.enabled"** |비트랜잭션 토폴로지에 대해 승인이 사용하도록 설정되는지 여부입니다. |

hello runspec 명령 hello 비트와 함께 배포 될, hello 사용과 같습니다.

    .\bin\runSpec.cmd
    usage: runSpec [spec-file target-dir [resource-dir] [-cp classpath]]
    ex: runSpec examples\HelloWorld\HelloWorld.spec specs examples\HelloWorld\Target

hello ***리소스-dir*** 매개 변수는 선택적, toospecify 필요한 tooplug C를 원하는 경우\# 응용 프로그램, 그리고이 디렉터리는 hello 응용 프로그램, hello 종속성 및 구성을 포함 됩니다.

hello ***classpath*** 도 매개 변수는 선택 사항입니다. Java Spout 또는 번개 hello 사양 파일을 포함 하는 경우 사용 되는 toospecify hello Java classpath입니다.

## <a name="miscellaneous-features"></a>기타 기능
### <a name="input-and-output-schema-declaration"></a>입력 및 출력 스키마 선언
hello 사용자 c에서 튜플을 내보낼 수\# 처리 하 고, hello 플랫폼 요구 사항을 tooserialize hello 튜플 byte, 전송 tooJava 쪽 스톰이 튜플 toohello 대상으로 전송 됩니다. 한편 다운스트림 구성 요소에서 C hello\# 프로세스 java 로부터 튜플을 수신 하 고 플랫폼별 toohello 원래 형식을 변환,이 작업은 모두 hello 플랫폼으로 숨겨져 있습니다.

toosupport hello serialization 및 deserialization toodeclare hello 스키마 hello 입력 및 출력의 사용자 코드에 필요합니다.

hello 입/출력 스트림 스키마 hello 키가 사전으로 정의 hello StreamId 고 hello 값은 hello 유형의 hello 열입니다. hello 구성 요소에는 선언 된 다중 스트림이 있을 수 있습니다.

    public class ComponentStreamSchema
    {
        public Dictionary<string, List<Type>> InputStreamSchema { get; set; }
        public Dictionary<string, List<Type>> OutputStreamSchema { get; set; }
        public ComponentStreamSchema(Dictionary<string, List<Type>> input, Dictionary<string, List<Type>> output)
        {
            InputStreamSchema = input;
            OutputStreamSchema = output;
        }
    }


컨텍스트 개체에 hello 다음 API를 추가 해야 합니다.

    public void DeclareComponentSchema(ComponentStreamSchema schema)

사용자 코드는 해당 스트림에 대해 정의 된 hello 스키마를 준수 하는 내보내는 hello 튜플 또는 hello 시스템은 런타임 예외를 throw 하는 있는지 확인 해야 합니다.

### <a name="multi-stream-support"></a>여러 스트림 지원
SCP 지원 사용자 tooemit 코드 또는 hello에 여러 가지 스트림에서 동일 수신 시간입니다. 선택적 스트림 ID 매개 변수를 사용 하는 hello Emit 메서드 hello 지원 hello 컨텍스트 개체의 내용을 반영 합니다.

두 가지 방법 hello SCP.NET 컨텍스트 개체에에서 추가 되었습니다. 사용 되는 tooemit 튜플 또는 튜플 toospecify StreamId 됩니다. hello StreamId는 문자열이 고 toobe 모두 C에서 일관성이 필요한\# 토폴로지 정의 사양 hello 및 합니다.

        /* Emit tuple toohello specific stream. */
        public abstract void Emit(string streamId, List<object> values);

        /* for non-transactional Spout only */
        public abstract void Emit(string streamId, List<object> values, long seqId);

내보내는 tooa 존재 하지 않는 스트림에 hello 런타임 예외를 발생 합니다.

### <a name="fields-grouping"></a>필드 그룹화
hello SCP.NET에 기본 제공 필드에에서 그룹화가 Strom 제대로 작동 하지 않습니다. Java 프록시 쪽 hello, 모든 hello 필드 데이터 형식이 실제로 byte, 않으며 hello 바이트 개체 해시 코드 tooperform hello 그룹을 사용 하 여 hello 필드를 그룹화 합니다. hello 바이트 개체 해시 코드는 메모리에서이 개체의 hello 주소입니다. Hello 그룹화 2 바이트에 대 한 잘못 된 되도록 해당 공유 hello 콘텐츠 동일 하지만 같은 주소 하지 hello 개체입니다.

SCP.NET 사용자 지정된 그룹화 메서드를 추가 하 고 hello 바이트 toodo hello 그룹화의 hello 콘텐츠를 사용 합니다. **사양** 파일 처럼은 hello 구문:

    (bolt-spec
        {
            "spout_test" (scp-field-group :non-tx [0,1])
        }
        …
    )


여기서 각 부분의 의미는 다음과 같습니다.

1. "scp-field-group"은 "SCP에서 구현하는 사용자 지정된 필드 그룹화"를 의미합니다.
2. ":tx" 또는 ":non-tx"는 트랜잭션 토폴로지인지 여부를 의미합니다. 시작 인덱스 hello tx가 아닌 토폴로지 및 다른 tx 이므로이 정보가 필요 합니다.
3. [0,1]은 0부터 시작하는 필드 ID의 해시 집합을 의미합니다.

### <a name="hybrid-topology"></a>하이브리드 토폴로지
Java로 작성 된 네이티브 스톰 번호입니다. SCP.Net가 향상 것 tooenable 및이 사용자 지정 toowrite C\# toohandle 해당 비즈니스 논리를 코딩 합니다. 그러나 C\# Spout/Bolt뿐 아니라 Java Spout/Bolt도 포함하는 하이브리드 토폴로지도 지원됩니다.

### <a name="specify-java-spoutbolt-in-spec-file"></a>사양 파일에서 Java Spout/Bolt 지정
사양 파일에 사용 되는 toospecify Java Spouts 및 볼트 "scp 배출구" 및 "scp 볼트" 일 수도 있습니다, 그리고 예를 들면 같습니다.

    (spout-spec 
      (microsoft.scp.example.HybridTopology.Generator.)           
      :p 1)

여기 `microsoft.scp.example.HybridTopology.Generator` hello hello Java Spout 클래스 이름입니다.

### <a name="specify-java-classpath-in-runspec-command"></a>runSpec 명령에서 Java 클래스 경로 지정
Java Spouts 또는 볼트 포함 된 toosubmit 토폴로지를 원하는 경우 Java Spouts toofirst 컴파일 hello 또는 볼트 필요 하 고 hello Jar 파일을 가져옵니다. 토폴로지를 전송할 때 hello Jar 파일을 포함 하는 hello java 클래스 경로 지정 합니다. 다음은 예제입니다.

    bin\runSpec.cmd examples\HybridTopology\HybridTopology.spec specs examples\HybridTopology\net\Target -cp examples\HybridTopology\java\target\*

여기 **예제\\HybridTopology\\java\\대상\\**  hello Java 배출구/볼트 Jar 파일 있는 hello 폴더입니다.

### <a name="serialization-and-deserialization-between-java-and-c"></a>Java와 C\ 간의 직렬화 및 역직렬화
SCP 구성 요소는 Java 쪽과 C\# 쪽을 포함합니다. 순서 toointeract 네이티브 Java Spouts/볼트와에서 Serialization/Deserialization를 수행 해야 Java 쪽와 C 간의\# hello 다음 그래프에에서 나타난 것 처럼 측면입니다.

![tooJava 구성 요소를 보내는 tooSCP 구성 요소를 보내는 java 구성 요소 다이어그램](media/hdinsight-storm-scp-programming-guide/java-compent-sending-to-scp-component-sending-to-java-component.png)

1. **Java 쪽의 직렬화 및 C\# 쪽의 역직렬화**
   
   먼저 Java 쪽의 직렬화와 C\# 쪽의 역직렬화를 위한 기본 구현이 제공됩니다. Java 쪽의 hello 직렬화 메서드 사양 파일에 지정할 수 있습니다.
   
       (scp-bolt
           {
               "plugin.name" "HybridTopology.exe"
               "plugin.args" ["displayer"]
               "output.schema" {}
               "customized.java.serializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer"]
           })
   
   C에서 deserialization 메서드 hello\# C 쪽으로 지정 해야\# 사용자 코드:
   
       Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
       inputSchema.Add("default", new List<Type>() { typeof(Person) });
       this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, null));
       this.ctx.DeclareCustomizedDeserializer(new CustomizedInteropJSONDeserializer());            
   
   Hello 데이터 형식이 너무 복잡 합니다. 아닌 경우이 기본 구현은 대부분의 경우를 처리 해야 합니다. 특정 한 경우에 대 한 하거나 hello 사용자 데이터 형식이 너무 복잡 하기 때문에 또는 hello 성능 기본 구현에 맞지 않으므로 hello 사용자의 요구 사항, 사용자 수 있는 플러그 인 고유한 구현 합니다.
   
   hello 직렬화 인터페이스 java 쪽으로 정의 됩니다.
   
       public interface ICustomizedInteropJavaSerializer {
           public void prepare(String[] args);
           public List<ByteBuffer> serialize(List<Object> objectList);
       }
   
   hello deserialize c에서 인터페이스\# 쪽으로 정의 됩니다.
   
   공용 인터페이스 ICustomizedInteropCSharpDeserializer
   
       public interface ICustomizedInteropCSharpDeserializer
       {
           List<Object> Deserialize(List<byte[]> dataList, List<Type> targetTypes);
       }
2. **C\# 쪽의 직렬화 및 Java 쪽의 역직렬화**
   
   C의 직렬화 메서드 hello\# C 쪽으로 지정 해야\# 사용자 코드:
   
       this.ctx.DeclareCustomizedSerializer(new CustomizedInteropJSONSerializer()); 
   
   hello Java 쪽에 Deserialization 메서드 사양 파일에 지정 해야 합니다.
   
     (scp-spout
   
       {
         "plugin.name" "HybridTopology.exe"
         "plugin.args" ["generator"]
         "output.schema" {"default" ["person"]}
         "customized.java.deserializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" "microsoft.scp.example.HybridTopology.Person"]
       })
   
   여기 "microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" 역직렬 변환기의 hello 이름 이므로 "microsoft.scp.example.HybridTopology.Person" hello 대상 클래스 hello 데이터를 deserialize 됩니다.
   
   사용자는 또한 C\# 직렬화 및 Java 역직렬화의 자체 구현을 플러그 인 할 수 있습니다. 이 C에 대 한 hello 인터페이스\# serializer.
   
       public interface ICustomizedInteropCSharpSerializer
       {
           List<byte[]> Serialize(List<object> dataList);
       }
   
   다음은 Java 역직렬 변환기에 대 한 hello 인터페이스입니다.
   
       public interface ICustomizedInteropJavaDeserializer {
           public void prepare(String[] targetClassNames);
           public List<Object> Deserialize(List<ByteBuffer> dataList);
       }

## <a name="scp-host-mode"></a>SCP 호스트 모드
이 모드에서는 사용자 자신의 코드 tooDLL 컴파일를 SCPHost.exe SCP toosubmit 토폴로지에서 제공 합니다. hello 사양 파일은 다음과 같습니다.

    (scp-spout
      {
        "plugin.name" "SCPHost.exe"
        "plugin.args" ["HelloWorld.dll" "Scp.App.HelloWorld.Generator" "Get"]
        "output.schema" {"default" ["sentence"]}
      })

여기에서 `plugin.name`은(는) SCP SDK에서 제공된 `SCPHost.exe`(으)로 지정됩니다. SCPHost.exe는 정확히 3개의 매개 변수를 허용합니다.

1. hello 먼저 하나는 hello DLL 이름이 며, `"HelloWorld.dll"` 이 예에서 합니다.
2. hello 두 번째 메서드는 hello 클래스 이름이 며, `"Scp.App.HelloWorld.Generator"` 이 예에서 합니다.
3. hello 셋째 하나 hello의 이름인 호출 된 tooget ISCPPlugin의 인스턴스 수 있는 공용 정적 메서드의 합니다.

호스트 모드에서 사용자 코드는 DLL로 컴파일되며 SCP 플랫폼에 의해 호출됩니다. 따라서 SCP 플랫폼 hello 전체 처리 논리의 모든 권한을 얻을 수 있습니다. 따라서 고객 toosubmit 토폴로지가 권장 SCP 호스트 모드에서 hello 개발 환경을 단순화 하 고 이후 릴리스도에 대 한 더 많은 유연성 및 이전 버전과 호환성을 더 잘 너는 수 있습니다.

## <a name="scp-programming-examples"></a>SCP 프로그래밍 예제
### <a name="helloworld"></a>HelloWorld
**HelloWorld** 아주 간단한 예제 tooshow SCP.Net 맛은 합니다. 여기에는 **generator**라는 Spout와 **splitter** 및 **counter**라는 Bolt 2개가 포함된 비트랜잭션 토폴로지가 사용됩니다. hello 배출구 **생성기** 임의로 일부 문장을 생성 하 고 이러한 문장 너무 내보낼 됩니다**분할자**합니다. hello 볼트 **분할자** hello 문장 toowords 분할 되며 이러한 단어를 너무 내보낼**카운터** 볼트 합니다. hello 볼트 "counter" 각 단어의 사전 toorecord hello 발생 번호를 사용합니다.

이 예제에는 **HelloWorld.spec** 및 **HelloWorld\_EnableAck.spec**의 두 가지 사양 파일이 있습니다. Hello C에서에서\# 코드 것 알아볼 수 hello pluginConf Java 쪽에서 가져와서 ack 활성화 되어 있는지 여부.

    /* demo how tooget pluginConf info */
    if (Context.Config.pluginConf.ContainsKey(Constants.NONTRANSACTIONAL_ENABLE_ACK))
    {
        enableAck = (bool)(Context.Config.pluginConf[Constants.NONTRANSACTIONAL_ENABLE_ACK]);
    }
    Context.Logger.Info("enableAck: {0}", enableAck);

사전은 ack를 사용 하는 hello 배출구에 사용 되는 toocache hello 튜플 했지만 되지 않은입니다. Fail() 호출 되 면 hello 실패 한 튜플 재생 됩니다.

    public void Fail(long seqId, Dictionary<string, Object> parms)
    {
        Context.Logger.Info("Fail, seqId: {0}", seqId);
        if (cachedTuples.ContainsKey(seqId))
        {
            /* get hello cached tuple */
            string sentence = cachedTuples[seqId];

            /* replay hello failed tuple */
            Context.Logger.Info("Re-Emit: {0}, seqId: {1}", sentence, seqId);
            this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new Values(sentence), seqId);
        }
        else
        {
            Context.Logger.Warn("Fail(), can't find cached tuple for seqId {0}!", seqId);
        }
    }

### <a name="helloworldtx"></a>HelloWorldTx
hello **HelloWorldTx** 예제 방법을 tooimplement 트랜잭션 토폴로지입니다. 이 예제에는 **generator** Spout, **partial-count** Batch Bolt 및 **count-sum** Commit Bolt가 있습니다. 또한 미리 작성된 txt 파일 **DataSource0.txt**, **DataSource1.txt** 및 **DataSource2.txt**의 세 개가 있습니다.

각 트랜잭션에서 배출구 hello **생성기** 임의로 3 개의 파일을 만들어 놓아야 hello에서 두 개의 파일을 선택 하 고 hello 두 파일 이름을 toohello 내보내는 됩니다 **부분 개수** 볼트 합니다. hello 볼트 **부분-c o u** 는 먼저 hello 파일 이름을 받은 hello 튜플 열려 hello 파일 및 count hello 단어 수에서이 파일에서 가져오고 hello 단어 번호 toohello 마지막으로 내보내기 **개수-sum**볼트 합니다. hello **count sum** 볼트 hello 총 수를 요약 합니다.

tooachieve **정확히 한 번만** 의미 체계, hello 커밋 볼트 **count sum** 재생된 트랜잭션 인지 toojudge 필요 합니다. 이 예제에서는 "count-sum"에 정적 멤버 변수가 있습니다.

    public static long lastCommittedTxId = -1; 

Hello ISCPBatchBolt 인스턴스를 만들 때 가져올 `txAttempt` 입력된 매개 변수에서:

    public static CountSum Get(Context ctx, Dictionary<string, Object> parms)
    {
        /* for transactional topology, we can get txAttempt from hello input parms */
        if (parms.ContainsKey(Constants.STORM_TX_ATTEMPT))
        {
            StormTxAttempt txAttempt = (StormTxAttempt)parms[Constants.STORM_TX_ATTEMPT];
            return new CountSum(ctx, txAttempt);
        }
        else
        {
            throw new Exception("null txAttempt");
        }
    }

때 `FinishBatch()` 호출 hello `lastCommittedTxId` 재생 된 트랜잭션이 면 업데이트 됩니다.

    public void FinishBatch(Dictionary<string, Object> parms)
    {
        /* judge whether it is a replayed transaction? */
        bool replay = (this.txAttempt.TxId <= lastCommittedTxId);

        if (!replay)
        {
            /* If it is not replayed, update hello toalCount and lastCommittedTxId vaule */
            totalCount = totalCount + this.count;
            lastCommittedTxId = this.txAttempt.TxId;
        }
        … …
    }


### <a name="hybridtopology"></a>HybridTopology
이 토폴로지는 Java Spout와 C\# Bolt를 포함하며, Hello 기본 serialization 및 deserialization 구현 SCP 플랫폼에서 제공을 사용 합니다. Ref hello 하세요 **HybridTopology.spec** 에 **예제\\HybridTopology** hello 사양 파일 세부 정보에 대 한 폴더 및 **SubmitTopology.bat** 방법에 대 한 toospecify Java classpath 합니다.

### <a name="scphostdemo"></a>SCPHostDemo
이 예에서는 기본적으로 HelloWorld 동일 hello. hello만 클래스 간의 차이점은 hello 사용자 코드를 DLL로 컴파일될 hello 토폴로지 SCPHost.exe를 사용 하 여 전송 됩니다. Ref hello "SCP 호스트 모드" 섹션에 대 한 자세한 설명은 하세요.

## <a name="next-steps"></a>다음 단계
SCP를 사용 하 여 만든 스톰 토폴로지 예 hello 다음 참조.

* [Visual Studio를 사용하여 HDInsight에서 Apache Storm에 대한 C# 토폴로지 개발](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [HDInsight의 Storm으로 Azure 이벤트 허브에서 이벤트 처리](hdinsight-storm-develop-csharp-event-hub-topology.md)
* [C# Storm 토폴로지에서 여러 데이터 스트림 만들기](hdinsight-storm-twitter-trending.md)
* [Power Bi toovisualize 데이터 스톰 토폴로지를 사용 하 여](hdinsight-storm-power-bi-topology.md)
* [HDInsight의 Storm을 사용하여 이벤트 허브에서 차량 센서 데이터 처리](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/IotExample)
* [추출, 변환 및 로드 (ETL) tooHBase Azure 이벤트 허브에서](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/RealTimeETLExample)
* [HDInsight에서 Storm 및 HBase를 사용하여 이벤트의 상관 관계 지정](hdinsight-storm-correlation-topology.md)

