---
title: "발생 한 aaaCommon FabricClient 예외 | Microsoft Docs"
description: "Hello 일반적인 예외와 응용 프로그램 및 클러스터 관리 작업을 수행 하는 동안 hello FabricClient Api에 의해 throw 될 수 있는 오류를 설명 합니다."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: bb821313-b221-479f-b08e-36cf07e60a07
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: ryanwi
ms.openlocfilehash: 55bb556b25150524ebc28756eb1bd3e91dc37853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="common-exceptions-and-errors-when-working-with-hello-fabricclient-apis"></a>일반적인 예외 및 오류 hello FabricClient Api로 작업 하는 경우
hello [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient#System_Fabric_FabricClient) Api 클러스터 및 응용 프로그램 관리자 tooperform 관리 작업을 서비스 패브릭 응용 프로그램, 서비스 또는 클러스터를 사용 합니다. 예를 들어 응용 프로그램 배포, 업그레이드 및 제거, hello 상태는 클러스터를 확인 하거나 서비스를 테스트 합니다. 응용 프로그램 개발자와 클러스터 관리자 hello 서비스 패브릭 클러스터 및 응용 프로그램을 관리 하기 위한 hello FabricClient Api toodevelop 도구를 사용할 수 있습니다.

FabricClient를 사용하여 수행할 수 있는 다양한 유형의 작업이 있습니다.  각 메서드에 tooincorrect 입력, 런타임 오류 또는 일시적인 인프라 문제 않아서 발생 한 오류에 대 한 예외를 throw 할 수 있습니다.  특정 메서드는 예외를 throw 하는 hello API 참조 설명서 toofind를 참조 하십시오. 그러나 여러 많은 [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient#System_Fabric_FabricClient) API에 의해 발생되는 몇몇 예외가 있습니다. hello 다음 표는 hello FabricClient Api 간에 공통 hello 예외입니다.

| 예외 | 발생 시점 |
| --- |:--- |
| [System.Fabric.FabricObjectClosedException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricobjectclosedexception#System_Fabric_FabricObjectClosedException) |hello [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient#System_Fabric_FabricClient) 개체가 닫혔습니다. Hello 삭제 [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient#System_Fabric_FabricClient) 사용 중이 고 새 개체 [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient#System_Fabric_FabricClient) 개체입니다. |
| [System.TimeoutException](https://docs.microsoft.com/dotnet/core/api/system.timeoutexception#System_TimeoutException) |hello 작업이 시간 초과 되었습니다. [Operationtimedout과](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode#System_Fabric_FabricErrorCode) 제한은 MaxOperationTimeout toocomplete 보다 많은 hello 작업을 수행 하는 경우 반환 됩니다. |
| [System.UnauthorizedAccessException](https://docs.microsoft.com/dotnet/core/api/system.unauthorizedaccessexception#System_UnauthorizedAccessException) |hello 작업에 대 한 hello 액세스 검사 하지 못했습니다. E_ACCESSDENIED가 반환됩니다. |
| [System.Fabric.FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception#System_Fabric_FabricException) |Hello 작업을 수행 하는 동안 런타임 오류가 발생 했습니다. Throw 잠재적으로 hello FabricClient 메서드 중 아무 메서드나 [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception#System_Fabric_FabricException), hello [ErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception#System_Fabric_FabricException_ErrorCode) 속성 hello 예외의 hello 정확한 원인을 나타냅니다. 오류 코드는 hello에 정의 된 [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode#System_Fabric_FabricErrorCode) 열거 합니다. |
| [System.Fabric.FabricTransientException](https://docs.microsoft.com/dotnet/api/system.fabric.fabrictransientexception#System_Fabric_FabricTransientException) |어떤 종류의 tooa 일시적인 오류 조건이 인해 hello 작업이 실패 했습니다. 예를 들어 복제본의 쿼럼에 일시적으로 연결할 수 없기 때문에 작업이 실패할 수 있습니다. 일시적인 예외 해당 toofailed 작업을 다시 시도할 수 있습니다. |

일부 일반 [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode#System_Fabric_FabricErrorCode) 오류는 [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception#System_Fabric_FabricException)으로 반환될 수 있습니다.

| 오류 | 조건 |
| --- |:--- |
| CommunicationError |통신 오류로 인해 hello 작업 toofail hello 작업을 다시 시도 합니다. |
| InvalidCredentialType |hello 자격 증명 유형이 잘못 되었습니다. |
| InvalidX509FindType |hello X509FindType 올바르지 않습니다. |
| InvalidX509StoreLocation |hello X509 저장소 위치가 올바르지 않습니다. |
| InvalidX509StoreName |hello X509 저장소 이름이 올바르지 않습니다. |
| InvalidX509Thumbprint |hello X509 인증서 지문 문자열이 올바르지 않습니다. |
| InvalidProtectionLevel |hello 보호 수준이 잘못 되었습니다. |
| InvalidX509Store |hello X509 인증서 저장소를 열 수 없습니다. |
| InvalidSubjectName |hello 주체 이름이 잘못 되었습니다. |
| InvalidAllowedCommonNameList |일반 이름 목록 문자열 hello 형식이 올바르지 않습니다. 쉼표로 구분된 목록이어야 합니다. |

