---
title: "PowerShell 사용 하 여 클라우드 서비스 컨테이너 aaaCreate | Microsoft Docs"
description: "이 문서에서는 클라우드 toocreate PowerShell 사용 하 여 컨테이너를 서비스 하는 방법을 설명 합니다. hello 컨테이너 웹 및 작업자 역할을 호스팅합니다."
services: cloud-services
documentationcenter: .net
author: cawaMS
manager: timlt
editor: 
ms.assetid: c8f32469-610e-4f37-a3aa-4fac5c714e13
ms.service: cloud-services
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 11/18/2016
ms.author: cawa
ms.openlocfilehash: 4c47b10b5ba1f9cc39594a45cd869bf04fcaadf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-an-azure-powershell-command-toocreate-an-empty-cloud-service-container"></a>Azure PowerShell 명령 toocreate 빈 클라우드 서비스 컨테이너를 사용 하 여
이 문서에서는 tooquickly Azure PowerShell cmdlet을 사용 하 여 클라우드 서비스 컨테이너를 만드는 방법에 대해 설명 합니다. 다음 hello 단계를 수행 하십시오.

1. Hello에서 hello Microsoft Azure PowerShell cmdlet 설치 [Azure PowerShell 다운로드](http://aka.ms/webpi-azps) 페이지.
2. Hello PowerShell 명령 프롬프트를 엽니다.
3. 사용 하 여 hello [Add-azureaccount](https://msdn.microsoft.com/library/dn495128.aspx) toosign에 있습니다.

   > [!NOTE]
   > Hello Azure PowerShell cmdlet 설치 및 연결 tooyour Azure 구독에 추가 명령에 대 한 참조 너무[어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.
   >
   >
4. 사용 하 여 hello **New-azureservice** cmdlet toocreate 빈 Azure 클라우드 서비스 컨테이너입니다.

    ```
    New-AzureService [-ServiceName] <String> [-AffinityGroup] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
    New-AzureService [-ServiceName] <String> [-Location] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
   ```
5. 이 예제에서는 tooinvoke hello cmdlet을 수행 합니다.

   ```
   New-AzureService -ServiceName "mytestcloudservice" -Location "Central US" -Label "mytestcloudservice"
   ```

Hello Azure 클라우드 서비스를 만드는 방법에 대 한 자세한 내용은 다음을 실행 합니다.

```
Get-help New-AzureService
```

### <a name="next-steps"></a>다음 단계
* toomanage hello 클라우드 서비스 배포, toohello 참조 [Get-azureservice](https://msdn.microsoft.com/library/azure/dn495131.aspx), [제거 AzureService](https://msdn.microsoft.com/library/azure/dn495120.aspx), 및 [집합 AzureService](https://msdn.microsoft.com/library/azure/dn495242.aspx) 명령입니다. 너무 나타낼 수도 있습니다[어떻게 tooconfigure 클라우드 서비스](cloud-services-how-to-configure.md) 자세한 정보.
* toopublish 클라우드 서비스 프로젝트 tooAzure, toohello 참조 **PublishCloudService.ps1** 코드 샘플을 [Azure의 클라우드 서비스에 대 한 지속적인 업데이트](cloud-services-dotnet-continuous-delivery.md)합니다.
