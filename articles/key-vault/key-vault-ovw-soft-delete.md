---
ms.assetid: 
title: "aaaAzure 주요 자격 증명 모음에 대 한 일시 삭제 | Microsoft Docs"
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/10/2017
ms.openlocfilehash: 1b402c58db6f25ae4ae5e2720786fa81eb0e839a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-soft-delete-overview"></a>Azure Key Vault 일시 삭제 개요

주요 자격 증명 모음의 일시 삭제 기능을 사용 하면 자격 증명 모음 삭제 hello 및 소프트 삭제 라고도 하는 자격 증명 모음 개체를 복구 합니다. 특히 다음 시나리오는 hello를 주소 했습니다.

- Key Vault의 복구 가능한 삭제 지원
- 주요 자격 증명 모음 개체(예: 키, 암호, 인증서)의 복구 가능한 삭제 지원

## <a name="supporting-interfaces"></a>인터페이스 지원

hello 소프트 삭제 하는 기능 초기에.NET hello REST 통해 C# 및 PowerShell 인터페이스 /입니다. 자세한 내용은 이러한 toohello 참조를 참조 [키 자격 증명 모음 참조](https://docs.microsoft.com/azure/key-vault/)합니다.

## <a name="scenarios"></a>시나리오

Azure Key Vault는 Azure Resource Manager에서 관리하는 추적된 리소스입니다. Azure Resource Manager는 삭제 작업에 성공할 경우 리소스에 더 이상 액세스할 수 없도록 요구하는 잘 정의된 삭제 동작도 지정합니다. hello 소프트 삭제 하는 기능 주소 여부에 관계 없이 hello 삭제 실수로 또는 의도적으로 삭제 하는 hello 개체의 복구를 hello 합니다.

1. Hello 일반적인 시나리오의 사용자 삭제 수 있습니다 실수로 주요 자격 증명 모음 또는 키 자격 증명 모음 개체입니다. 해당 키 자격 증명 모음 또는 키 자격 증명 모음 개체 toobe 미리 결정 된 기간에 대 한 복구 된 경우 hello 사용자 hello 삭제를 취소할를 업데이트 하 고 해당 데이터를 복구할 수 있습니다.

2. 다른 시나리오에서는 rogue 사용자는 주요 자격 증명 모음 또는 자격 증명 모음, 비즈니스 중단 toocause 내 키와 같은 키 자격 증명 모음 개체를 toodelete를 시도할 수 있습니다. 안전 조치 by, 예를 들어, 데이터 삭제 tooa 다른 경우에 대해 권한을 제한할 신뢰할 수 있는 역할 처럼 hello 주요 자격 증명 모음 또는 키 자격 증명 모음 개체의 hello 삭제 hello 내부 데이터의 실제 삭제 hello에서에서 분리를 사용할 수 있습니다. 이 접근법에는 즉각적인 데이터 손실을 초래할 수 있는 작업에 대한 쿼럼이 필요합니다.

### <a name="soft-delete-behavior"></a>일시 삭제 동작

이 기능을 hello 주요 자격 증명 모음에 대해 DELETE 작업 또는 키 자격 증명 모음 개체는 delete-소프트를 효과적으로 hello 모양 hello 개체를 제공을 삭제 하는 동안 지정 된 보존 기간에 대 한 hello 리소스를 보유 합니다. hello 서비스를 더욱 기본적으로 hello 삭제를 취소 하는 개체를 삭제 hello를 복구 하기 위한 메커니즘을 제공 합니다. 

일시 삭제는 선택적 Key Vault 동작이며, 이 릴리스에서 **기본적으로 사용되지 않습니다**. 주요 자격 증명 모음에 대 한 일시 삭제를 사용 하면 참조의 선택한 hello 인터페이스에 대 한 hello 참조 hello 구체적인 지침은 [키 자격 증명 모음 참조](https://docs.microsoft.com/azure/key-vault/)합니다.

### <a name="key-vault-recovery"></a>주요 자격 증명 모음 복구

주요 자격 증명 모음 삭제 시 hello 서비스 복구를 위한 충분 한 메타 데이터를 추가 하는 hello 구독에서 프록시 리소스를 만듭니다. hello 프록시 리소스 hello에서 사용할 수 있는 저장 된 개체는 삭제 hello 키 자격 증명 모음과 동일한 위치입니다. 

### <a name="key-vault-object-recovery"></a>주요 자격 증명 모음 개체 복구

예: 키, 키 자격 증명 모음 개체 삭제 시 hello 서비스는 배치 hello 개체 삭제 된 상태에서 하므로 액세스할 수 없는 tooany 검색 작업 합니다. 이 상태 동안에 hello 주요 자격 증명 모음 개체가 수만 목록에 복구 된, 또는 강제로/영구적으로 삭제 합니다. 

Hello에서 동일한 시간, 키 자격 증명 모음에서는 일정 데이터 해당 toohello 삭제 기본 hello hello 삭제 주요 자격 증명 모음 또는 미리 결정 된 보존 간격 후에 실행에 대 한 주요 자격 증명 모음 개체입니다. hello DNS 레코드 해당 toohello 자격 증명 모음 hello hello 보존 간격 동안에도 유지 됩니다.

### <a name="soft-delete-retention-period"></a>일시 삭제 보존 기간

일시 삭제된 리소스는 설정된 기간, 즉 90일 동안 유지됩니다. Hello 소프트 삭제 보존 간격 동안 hello 다음 적용 됩니다.

- 모든 hello 키 자격 증명 모음 및 키 자격 증명 모음 개체에 대 한 액세스를 삭제 하 고 복구 정보 뿐만 아니라 사용자 구독에 대 한 hello 일시 삭제 상태에 나열할 수 있습니다.
    - 특수 사용 권한이 있는 사용자만 삭제된 자격 증명 모음을 나열할 수 있습니다. 사용자가 삭제된 자격 증명 모음 처리를 위해 이러한 특수 사용 권한을 가진 사용자 지정 역할을 만드는 것이 좋습니다.
- 주요 자격 증명 모음 이름이 같은 hello에서 만들 수 없으므로 hello로 동일한 위치; 마찬가지로 키 자격 증명 모음 개체를 만들 수 없습니다 지정 된 자격 증명 모음에 해당 키 자격 증명 모음 hello로 개체가 있는 경우 동일한 이름 및 삭제 된 상태에 
- 특히 권한 있는 사용자만 hello 해당 프록시 리소스에 대해 복구 명령을 실행 하 여 주요 자격 증명 모음 또는 키 자격 증명 모음 개체를 복원할 수 있습니다.
    - hello 사용자 hello 권한 toocreate hello 리소스 그룹 아래의 주요 자격 증명 모음에 있는 hello 사용자 지정 역할의 멤버는 hello 자격 증명 모음을 복원할 수 있습니다.
- 특히 권한 있는 사용자만 키 자격 증명 모음 또는 키 자격 증명 모음 개체를 해당 프록시 리소스 hello에 delete 명령을 실행 하 여 강제로 삭제할 수 있습니다.

주요 자격 증명 모음 또는 키 자격 증명 모음 개체를 복구 하지 않는 한 hello에 hello 보존 간격 hello 서비스의 끝 hello 일시 삭제 된 주요 자격 증명 모음 또는 키 자격 증명 모음 개체와 해당 내용을 제거를 수행 합니다. 리소스 삭제를 다시 예약하지 못할 수 있습니다.

### <a name="permitted-purge"></a>허용된 제거

영구적으로 삭제, 제거, 주요 자격 증명 모음 수 hello 프록시 리소스에서 POST 작업을 통해 있으며 특별 한 권한이 필요 합니다. 일반적으로 구독 소유자만 hello 수 toopurge 주요 자격 증명 모음 됩니다. hello POST 작업 트리거 hello 즉각적이 고 복구할 수 없는 해당 자격 증명 모음을 삭제 합니다. 

예외 toothis hello 때는 Azure 구독 hello로 표시 되었습니다 *삭제할 수 없는*합니다. 이 경우에 hello 서비스는 hello 실제 삭제 후 수행 될 수 있습니다 하 고 예약 된 과정으로이 작업을 수행 합니다. 



