---
title: "Azure microservices의 aaaChange KVSActorStateProvider 설정 | Microsoft Docs"
description: "'KVSActorStateProvider' 형식의 Azure 서비스 패브릭 상태 저장 행위자를 구성하는 방법에 대해 알아봅니다."
services: Service-Fabric
documentationcenter: .net
author: sumukhs
manager: timlt
editor: 
ms.assetid: dbed72f4-dda5-4287-bd56-da492710cd96
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/29/2017
ms.author: sumukhs
ms.openlocfilehash: e003512678556e68a8926b1b9c6c28d9ae3979d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-reliable-actors--kvsactorstateprovider"></a>Reliable Actors 구성--KVSActorStateProvider
KVSActorStateProvider의 기본 구성은 hello hello Microsoft Visual Studio 패키지 루트 hello 지정 된 작업자에 대해 hello Config 폴더에서 생성 되는 hello settings.xml 파일을 변경 하 여 수정할 수 있습니다.

hello Azure 서비스 패브릭 런타임을 hello settings.xml 파일에 미리 정의 된 섹션 이름을 찾는 하 고 hello 기본 런타임 구성 요소를 만드는 동안 hello 구성 값을 사용 합니다.

> [!NOTE]
> 수행 **하지** 삭제 하거나 hello Visual Studio 솔루션에서에서 생성 되는 hello settings.xml 파일에는 구성을 따르고 hello의 hello 섹션 이름을 수정 합니다.
> 
> 

## <a name="replicator-security-configuration"></a>복제자 보안 구성
복제기 보안 구성을 복제 하는 동안 사용 되는 사용 되는 toosecure hello 통신 채널 됩니다. 즉, 서비스 다른 사용자의 복제 트래픽을 인지 확인 하는 hello는 데이터에 항상 사용 가능한도 보안을 볼 수 없습니다.
기본적으로 빈 보안 구성 섹션에서는 복제 보안이 되지 않습니다.

### <a name="section-name"></a>섹션 이름
&lt;ActorName&gt;ServiceReplicatorSecurityConfig

## <a name="replicator-configuration"></a>복제자 구성
복제기 구성 hello 행위자 상태 공급자 상태 안정성이 높아야 하는 일을 담당 하는 hello 복제기를 구성 합니다.
hello 기본 구성에서 hello Visual Studio 템플릿이 생성 되 고 충분 합니다. 이 섹션은 사용할 수 있는 tootune hello 복제기 추가 구성에 대 한 설명입니다.

### <a name="section-name"></a>섹션 이름
&lt;ActorName&gt;ServiceReplicatorConfig

### <a name="configuration-names"></a>구성 이름
| 이름 | 단위 | 기본값 | 설명 |
| --- | --- | --- | --- |
| BatchAcknowledgementInterval |초 |0.015 |Hello 보조 대기를 보내기 전에 다시 승인을 toohello 기본 작업을 받은 후에 hello 복제기에 대 한 시간 간격입니다. 이 간격 내에서 처리 하는 작업에 대 한 보낸 승인 toobe 하나의 응답으로 전송 됩니다. |
| ReplicatorEndpoint |해당 없음 |기본값 없음--필수 매개 변수 |IP 주소와 포트를 주/보조 복제기 hello toocommunicate hello 복제 세트에 다른 복제기를 사용 합니다. 이 서비스 매니페스트의 hello TCP 리소스 끝점을 참조 해야 합니다. 너무 참조[서비스 매니페스트 리소스](service-fabric-service-manifest-resources.md) tooread hello 서비스 매니페스트에 끝점 리소스를 정의 하는 방법에 대 한 자세한 합니다. |
| RetryInterval |초 |5 |기간이 지난 후 어떤 hello 복제기 다시 전송 작업에 대 한 승인을 받지 않을 경우 메시지입니다. |
| MaxReplicationMessageSize |바이트 |50MB |단일 메시지에서 전송할 수 있는 복제 데이터의 최대 크기. |
| MaxPrimaryReplicationQueueSize |작업의 수 |1024 |Hello 기본 큐에서 작업의 최대 수입니다. Hello 기본 복제기에서 모든 hello 보조 복제기에서 승인을 받은 후에 작업을 해제 됩니다. 이 값은 64보다 크고 2의 제곱이어야 합니다. |
| MaxSecondaryReplicationQueueSize |작업의 수 |2048 |Hello 보조 큐에 있는 작업의 최대 수입니다. 작업은 지속성을 통해 상태를 항상 사용 가능하도록 설정한 후 해제됩니다. 이 값은 64보다 크고 2의 제곱이어야 합니다. |

## <a name="store-configuration"></a>저장소 구성
저장소 구성이 사용 되는 tooconfigure hello 로컬 저장소에 복제 되 고 사용 되는 toopersist hello 상태가 됩니다.
hello 기본 구성에서 hello Visual Studio 템플릿이 생성 되 고 충분 합니다. 이 섹션 추가 구성에 사용할 수 있는 tootune hello에 대 한 로컬 저장소에 대해 소개 합니다.

### <a name="section-name"></a>섹션 이름
&lt;ActorName&gt;ServiceLocalStoreConfig

### <a name="configuration-names"></a>구성 이름
| 이름 | 단위 | 기본값 | 설명 |
| --- | --- | --- | --- |
| MaxAsyncCommitDelayInMilliseconds |밀리초 |200 |Hello 최대 일괄 처리 커밋 로컬 영 속 저장소에 대 한 간격을 설정 합니다. |
| MaxVerPages |페이지 수 |16384 |데이터베이스를 저장 하는 hello 최대 로컬 hello에 버전 페이지 수입니다. Hello 처리 중인 트랜잭션의 최대 수를 결정합니다. |

## <a name="sample-configuration-file"></a>샘플 구성 파일
```xml
<?xml version="1.0" encoding="utf-8"?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Section Name="MyActorServiceReplicatorConfig">
      <Parameter Name="ReplicatorEndpoint" Value="MyActorServiceReplicatorEndpoint" />
      <Parameter Name="BatchAcknowledgementInterval" Value="0.05"/>
   </Section>
   <Section Name="MyActorServiceLocalStoreConfig">
      <Parameter Name="MaxVerPages" Value="8192" />
   </Section>
   <Section Name="MyActorServiceReplicatorSecurityConfig">
      <Parameter Name="CredentialType" Value="X509" />
      <Parameter Name="FindType" Value="FindByThumbprint" />
      <Parameter Name="FindValue" Value="9d c9 06 b1 69 dc 4f af fd 16 97 ac 78 1e 80 67 90 74 9d 2f" />
      <Parameter Name="StoreLocation" Value="LocalMachine" />
      <Parameter Name="StoreName" Value="My" />
      <Parameter Name="ProtectionLevel" Value="EncryptAndSign" />
      <Parameter Name="AllowedCommonNames" Value="My-Test-SAN1-Alice,My-Test-SAN1-Bob" />
   </Section>
</Settings>
```
## <a name="remarks"></a>설명
hello BatchAcknowledgementInterval 매개 변수는 복제 대기 시간을 제어합니다. 값이 '0' (더 많은 승인 메시지를 전송 및 처리를 각각 포함 된 더 적은 승인 해야)으로 hello 가능한 최저의 대기 시간, 처리량의 hello 비용이 발생 합니다.
hello, BatchAcknowledgementInterval에 더 큰 hello 값 hello 더 높은 hello 전반적인 hello 비용을 더 높은 작업 대기 시간에 복제 처리량입니다. 트랜잭션 커밋의 대기 시간 toohello 직접 변환 됩니다.

