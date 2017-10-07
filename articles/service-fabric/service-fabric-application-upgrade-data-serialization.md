---
title: "응용 프로그램 업그레이드: 데이터 직렬화 | Microsoft Docs"
description: "데이터 직렬화 모범 사례 및 응용 프로그램 업그레이드 배포에 미치는 영향"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: a5f36366-a2ab-4ae3-bb08-bc2f9533bc5a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 1b65dfd3813423550631490640a81953864f58e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-data-serialization-affects-an-application-upgrade"></a>데이터 serialization이 응용 프로그램 업그레이드에 미치는 영향
에 [롤링 응용 프로그램 업그레이드](service-fabric-application-upgrade.md), hello 업그레이드가 적용된 tooa 노드의 하위 집합을 한 번에 하나의 업그레이드 도메인입니다. 이 과정에서 몇 가지 업그레이드 도메인 hello 최신 버전의 응용 프로그램에 있으며 hello 이전 버전의 응용 프로그램에 몇 가지 업그레이드 도메인은 합니다. Hello 롤아웃 중 hello 새 버전의 응용 프로그램, 데이터의 수 tooread hello 이전 버전 이어야 합니다. 및 hello 이전 버전의 응용 프로그램 수 tooread hello 새 버전의 데이터 여야 합니다. Hello 데이터 형식이 앞 이나 뒤로 hello 업그레이드가 호환 되지 않는 경우 수 실패, 또는 데이터 있습니다 수 손실 또는 손상 합니다. 이 문서에서는 데이터 서식을 구성하는 요소에 대해 설명하며 데이터가 상위 버전 및 하위 버전과 호환되도록 하는 모범 사례를 제공합니다.

## <a name="what-makes-up-your-data-format"></a>데이터 형식을 구성하는 요소
Azure 서비스 패브릭에서 hello 데이터 유지 되 고 복제는 C# 클래스에서 제공 합니다. 사용 하는 응용 프로그램에 대 한 [신뢰할 수 있는 컬렉션](service-fabric-reliable-services-reliable-collections.md), 데이터를 신뢰할 수 있는 사전 hello 및 큐에 있는 hello 개체입니다. 사용 하는 응용 프로그램에 대 한 [Reliable Actors](service-fabric-reliable-actors-introduction.md), hello 작업자에 대 한 상태를 백업 하는 hello 즉 합니다. 이러한 C# 클래스를 직렬화 해야 toobe 유지 하 고 복제 합니다. 따라서 hello 데이터 형식은 hello 필드와 속성을 serialize 되 면도 serialize 되는 방식으로 정의 됩니다. 예를 들어, 한 `IReliableDictionary<int, MyClass>` hello 데이터는 serialize 된 `int` 는 serialize 된 및 `MyClass`합니다.

### <a name="code-changes-that-result-in-a-data-format-change"></a>데이터 형식 변경이 발생하는 코드 변경
Hello 데이터 형식은 C# 클래스에 의해 결정 됩니다, 이후 데이터 형식 변경이 변경 toohello 클래스에 발생할 수 있습니다. 주의 해야 롤링 업그레이드를 처리할 수 있는 tooensure hello 데이터 형식을 변경 합니다. 다음은 데이터 형식이 변경될 수 있는 예입니다.

* 필드/속성 추가 또는 제거
* 필드 또는 속성의 이름 변경
* 필드 또는 속성의 hello 형식 변경
* Hello 클래스 이름 또는 네임 스페이스 변경

### <a name="data-contract-as-hello-default-serializer"></a>기본 serializer hello으로 데이터 계약
hello serializer는 일반적으로를 hello 데이터를 읽는 hello 현재 버전으로 역직렬화 하는 동안 hello 데이터를 이전에 있더라도 또는 *최신* 버전입니다. hello 기본 serializer는 hello [데이터 계약 serializer](https://msdn.microsoft.com/library/ms733127.aspx)를 잘 정의 된 버전 관리 규칙이 있습니다. 신뢰할 수 있는 컬렉션 수를 재정의 하는 hello serializer toobe 하지만 Reliable Actors 현재 하지 않습니다. 롤링 업그레이드를 사용 하기 위한 중요 한 역할 hello 데이터 직렬 변환기입니다. hello 데이터 계약 직렬화 기는 서비스 패브릭 응용 프로그램에 대해 권장 하는 hello serializer입니다.

## <a name="how-hello-data-format-affects-a-rolling-upgrade"></a>Hello 데이터 형식을 롤링 업그레이드에 미치는 영향
롤링 업그레이드는 두 가지 주요 시나리오 hello serializer 이전 발생할 수 또는 *최신* 데이터 버전:

1. 노드를 업그레이드 하 고 다시 시작, 후 hello 새 serializer hello 했던 데이터를 지속형된 toodisk hello 이전 버전에서 로드 됩니다.
2. 롤링 업그레이드 hello, 하는 동안 hello 클러스터 hello 이전 및 새 버전의 코드를 혼합 하 여 포함 됩니다. 복제본은 서로 다른 업그레이드 도메인에 배치 될 수 있습니다 하 고 복제본이 보낼 데이터 tooeach 다른 hello 새 및/또는 이전 버전의 데이터는 사용자 serializer의 hello 새 및/또는 이전 버전에서 발생할 수 있습니다.

> [!NOTE]
> "새 버전" 및 "이전 버전" hello 여기 toohello 버전의 실행 중인 코드를 참조 합니다. "새 serializer" hello hello 새 버전의 응용 프로그램에서 실행 되는 toohello serializer 코드를 참조 합니다. "새 데이터" hello hello 새 버전의 응용 프로그램에서 직렬화 toohello C# 클래스를 참조합니다.
> 
> 

코드의 두 버전 hello 및 앞으로 및 뒤로 데이터 형식 이어야 호환 됩니다. 호환 되지 않으므로, 롤링 업그레이드 hello에 오류가 발생 하거나 데이터가 손실 될 수 있습니다. hello 코드 또는 serializer가 throw 될 수 있습니다 예외 또는 오류 hello를 발견 한 경우 다른 버전 hello 롤링 업그레이드가 실패할 수 있습니다. 예를 들어 새 속성이 추가 되었습니다 하지만 hello 이전 serializer 역직렬화 하는 동안 삭제 하는 경우 데이터가 손실 될 수 있습니다.

데이터 계약은 hello 권장 데이터를 호환을 위한 솔루션입니다. 데이터 계약에는 필드의 추가, 제거 및 변경에 대해 잘 정의된 버전 관리 규칙이 있습니다. 알 수 없는 필드를 다루는 hello serialization 및 deserialization 프로세스에 연결 하 고 클래스 상속을 다루는 대 한 지원을 포함 합니다. 자세한 내용은 [데이터 계약 사용](https://msdn.microsoft.com/library/ms733127.aspx)을 참조하세요.

## <a name="next-steps"></a>다음 단계
[Visual Studio를 사용하여 응용 프로그램 업그레이드](service-fabric-application-upgrade-tutorial.md) 에서는 Visual Studio를 사용하여 응용 프로그램 업그레이드를 진행하는 방법을 안내합니다.

[Powershell을 사용하여 응용 프로그램 업그레이드](service-fabric-application-upgrade-tutorial-powershell.md) 에서는 PowerShell을 사용하여 응용 프로그램 업그레이드를 진행하는 방법을 안내합니다.

[업그레이드 매개 변수](service-fabric-application-upgrade-parameters.md)를 사용하여 응용 프로그램 업그레이드 방법을 제어합니다.

Toouse 너무 참조 하 여 응용 프로그램을 업그레이드 하는 동안 기능에 고급 하는 방법에 대해 알아봅니다[고급 항목](service-fabric-application-upgrade-advanced.md)합니다.

toohello 단계를 참조 하 여 응용 프로그램 업그레이드의 일반적인 문제를 수정 [응용 프로그램 업그레이드 문제 해결 ](service-fabric-application-upgrade-troubleshooting.md)합니다.

