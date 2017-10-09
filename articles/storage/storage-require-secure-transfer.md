---
title: "Azure 저장소에 안전 하 게 전송 aaaRequire | Microsoft Docs"
description: "Azure 저장소에 대 한 hello \"보안 전송 필요\" 기능에 대 한 자세한 내용은 방법과 tooenable 것입니다."
services: storage
documentationcenter: na
author: fhryo-msft
manager: Jason.Hogg
editor: fhryo-msft
ms.assetid: 
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 06/20/2017
ms.author: fryu
ms.openlocfilehash: 27f745c5e771b50213c1dbb39dee081947be1f39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="require-secure-transfer"></a>보안 전송 필요

hello "보안 전송 필요" 옵션만 toohello 저장소 계정에서 보안 연결 요청을 허용 하 여 저장소 계정의 hello 보안이 향상 됩니다. 예를 들어, REST Api tooaccess 저장소 계정의 호출할 때 HTTPS를 사용 하 여 연결 해야 합니다. "보안 전송 필요"가 설정된 경우 HTTP를 사용한 모든 요청이 거부됩니다.

Hello Azure 파일 서비스를 사용 하는 암호화 되지 않은 모든 연결 실패 "보안 전송 필요"를 사용 하도록 설정 합니다. SMB 2.1, SMB 3.0 암호화 없이 및 일부 버전의 Linux SMB 클라이언트 hello 사용 하는 시나리오를 포함 합니다. 

기본적으로 hello "보안 전송 필요" 옵션이 비활성화 됩니다.

> [!NOTE]
> Azure Storage에서 사용자 지정 도메인 이름에 대해 HTTPS를 지원하지 않으므로 사용자 지정 도메인 이름을 사용할 때 이 옵션이 적용되지 않습니다.

## <a name="enable-secure-transfer-required-in-hello-azure-portal"></a>"보안 전송 필요" hello Azure 포털에서에서 사용 하도록 설정

Hello "보안 전송 필요" hello에서 저장소 계정을 만들 때 모두 설정 되지 않는 것이 가능 [Azure 포털](https://portal.azure.com), 및 기존 저장소 계정에 대 한 합니다.

### <a name="require-secure-transfer-when-you-create-a-storage-account"></a>저장소 계정을 만들 때 보안 전송 필요

1. 열기 hello **저장소 계정 만들기** 블레이드 hello Azure 포털의에서.
1. **보안 전송 필요** 아래에서 **사용**을 선택합니다.

  ![스크린샷](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_1.png)

### <a name="require-secure-transfer-for-an-existing-storage-account"></a>기존 저장소 계정에 대해 보안 전송 필요

1. Hello Azure 포털에서에서 기존 저장소 계정을 선택 합니다.
1. 선택 **구성** 아래 **설정을** hello 저장소 계정 메뉴 블레이드에서 합니다.
1. **보안 전송 필요** 아래에서 **사용**을 선택합니다.

  ![스크린샷](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_2.png)

## <a name="enable-secure-transfer-required-programmatically"></a>프로그래밍 방식으로 "보안 전송 필요" 사용

hello 설정 이름은 _supportsHttpsTrafficOnly_ 저장소 계정 속성에서 합니다. REST API, 도구 또는 라이브러리를 사용하여 "보안 전송 필요" 설정을 사용할 수 있습니다.

* **REST API**(버전: 2016-12-01): [릴리스 패키지](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts)
* **PowerShell**(버전: 4.1.0): [릴리스 패키지](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0)
* **CLI**(버전: 2.0.11): [릴리스 패키지](https://pypi.python.org/pypi/azure-cli-storage/2.0.11)
* **NodeJS**(버전: 1.1.0): [릴리스 패키지](https://www.npmjs.com/package/azure-arm-storage/)
* **.NET SDK**(버전: 6.3.0): [릴리스 패키지](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview)
* **Python SDK**(버전: 1.1.0): [릴리스 패키지](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0)
* **Ruby SDK**(버전: 0.11.0): [릴리스 패키지](https://rubygems.org/gems/azure_mgmt_storage)

### <a name="enable-secure-transfer-required-setting-with-rest-api"></a>REST API를 사용하여 "보안 전송 필요" 설정 사용

REST API를 사용 하 여 테스트 toosimplify 사용할 수 있습니다 [ArmClient](https://github.com/projectkudu/ARMClient) toocall 명령줄에서.

 아래 명령줄 hello REST API를 사용 하는 toocheck hello 설정을 사용할 수 있습니다.

```
# Login Azure and proceed with your credentials
> armclient login

> armclient GET  /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01
```

Hello에 대 한 응답을 찾을 수 있습니다 _supportsHttpsTrafficOnly_ 설정 합니다. 샘플:

```Json
{
  "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}",
  "kind": "Storage",
  ...
  "properties": {
    ...
    "supportsHttpsTrafficOnly": false
  },
  "type": "Microsoft.Storage/storageAccounts"
}
```

아래 명령줄 hello REST API를 사용 하는 tooenable hello 설정을 사용할 수 있습니다.

```
# Login Azure and proceed with your credentials
> armclient login

> armclient PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01 < Input.json
```
Input.json의 샘플:
```Json
{
  "location": "westus",
  "properties": {
    "supportsHttpsTrafficOnly": true
  }
}
```

## <a name="next-steps"></a>다음 단계
Azure 저장소는 다양 한 개발자를 함께 사용 하는 보안 기능을 toobuild 보안 응용 프로그램을 제공 합니다. 자세한 내용은 방문 hello [저장소 보안 가이드](storage-security-guide.md)합니다.
