---
title: "aaaGuest OS 제품군 1 사용 중지 확인 | Microsoft Docs"
description: "Hello Azure 게스트 OS 제품군 1 사용 중지 발생 한 시기와 방법에 대 한 정보를 제공 하는 경우 toodetermine"
services: cloud-services
documentationcenter: na
author: raiye
manager: timlt
editor: 
ms.assetid: 37b422e9-0713-4a81-a942-f553ef478064
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 5/21/2017
ms.author: raiye
ms.openlocfilehash: fa8b904c6560dbbe4982c301f818c7a5cbc4eacb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="guest-os-family-1-retirement-notice"></a>게스트 OS 제품군 1 사용 중지 확인
hello OS 제품군 1 사용 중지는 2013 년 6 월 1 일에 처음 발표 되었습니다.

**2014 년 9 월 2 일** hello Azure 게스트 운영 체제 (게스트 OS) 제품군 1.x hello Windows Server 2008 운영 체제를 기반 하는 공식적으로 사용 중지 되었습니다. 모든 시도 toodeploy 새로운 서비스 또는 제품군 1을 사용 하 여 업그레이드 기존 서비스는 게스트 OS 제품군 1이 더 이상 해당 hello를 알리는 오류 메시지와 함께 실패 합니다.

**2014년 11월 3일** 게스트 OS 제품군 1에 대한 연장 지원이 종료되어 완전히 사용 중지됩니다. 제품군 1의 모든 서비스에 적용됩니다. 언제든지 이러한 서비스를 중지할 수 있습니다. 서비스는 수동으로 업그레이드 하지 않으면 해당 사용자가 직접 toorun 계속 보장이 없습니다.

추가 질문이 있으면 방문 hello [클라우드 서비스 포럼](http://social.msdn.microsoft.com/Forums/home?forum=windowsazuredevelopment&filter=alltypes&sort=lastpostdesc) 또는 [Azure 지원에 문의](https://azure.microsoft.com/support/options/)합니다.

## <a name="are-you-affected"></a>영향을 받나요?
클라우드 서비스는 hello 다음 중 하나에 적용 되는 경우 영향을 받습니다.

1. 값이 있는 "osFamily ="1"클라우드 서비스에 대 한 hello ServiceConfiguration.cscfg 파일에 명시적으로 지정 합니다.
2. 클라우드 서비스에 대 한 hello ServiceConfiguration.cscfg 파일에 명시적으로 지정 된 osFamily에 대 한 값을 않아도 됩니다. 현재, hello 시스템은이 경우 "1"의 hello 기본값을 사용합니다.
3. hello Azure 포털 게스트 운영 체제 제품군 값이 "Windows Server 2008"로 표시 합니다.

클라우드 서비스가 어떤 OS 제품군을 실행 하는 toofind, 해야 하지만 hello 다음 Azure PowerShell에서 스크립트를 실행할 수 있습니다 [Azure PowerShell을 설정](/powershell/azureps-cmdlets-docs) 첫 번째입니다. Hello 스크립트에 대 한 자세한 내용은 참조 하십시오. [Azure 게스트 OS 제품군 1 만료: 2014 년 6 월](http://blogs.msdn.com/b/ryberry/archive/2014/04/02/azure-guest-os-family-1-end-of-life-june-2014.aspx)합니다.

```Powershell
foreach($subscription in Get-AzureSubscription) {
    Select-AzureSubscription -SubscriptionName $subscription.SubscriptionName

    $deployments=get-azureService | get-azureDeployment -ErrorAction Ignore | where {$_.SdkVersion -NE ""}

    $deployments | ft @{Name="SubscriptionName";Expression={$subscription.SubscriptionName}}, ServiceName, SdkVersion, Slot, @{Name="osFamily";Expression={(select-xml -content $_.configuration -xpath "/ns:ServiceConfiguration/@osFamily" -namespace $namespace).node.value }}, osVersion, Status, URL
}
```

Hello 스크립트 출력의 osFamily 열 hello 비어 있거나 "1"을 포함 하는 경우 클라우드 서비스가 OS 제품군 1 사용 중지 알고 있어야 합니다.

## <a name="recommendations-if-you-are-affected"></a>영향을 받는 경우 권장 사항
Hello 지원 게스트 OS 제품군의 클라우드 서비스 역할 tooone 프로그램을 마이그레이션하는 것이 좋습니다.

**게스트 OS 제품군 4.x** -Windows Server 2012 R2 *(권장)*

1. 응용 프로그램이.NET framework 4.0, 4.5 또는 4.5.1과 함께 SDK 2.1 이상을 사용 중이어야 합니다.
2. Hello osFamily 특성이 너무 "4"에 hello ServiceConfiguration.cscfg 파일을 설정 하 고 클라우드 서비스를 다시 배포 합니다.

**게스트 OS 제품군 3.x** -Windows Server 2012

1. 응용 프로그램이.NET framework 4.0 또는 4.5와 함께 SDK 1.8 이상을 사용 중이어야 합니다.
2. Hello osFamily 특성이 너무 "3"에 hello ServiceConfiguration.cscfg 파일을 설정 하 고 클라우드 서비스를 다시 배포 합니다.

**게스트 OS 제품군 2.x** -Windows Server 2008 R2

1. 응용 프로그램이.NET framework 3.5 또는 4.0과 함께 SDK 1.3 이상을 사용 중이어야 합니다.
2. Hello osFamily 특성이 너무 "2"에 hello ServiceConfiguration.cscfg 파일을 설정 하 고 클라우드 서비스를 다시 배포 합니다.

## <a name="extended-support-for-guest-os-family-1-ended-nov-3-2014"></a>게스트 OS 제품군 1에 대한 연장된 지원이 2014년 11월 3일에 종료되었습니다.
게스트 OS 제품군 1에서 클라우드 서비스는 더 이상 지원 되지 않습니다. 제품군 1 제거 가능한 tooavoid 서비스 중단으로 마이그레이션하십시오.  

## <a name="next-steps"></a>다음 단계
검토 hello 최신 [게스트 OS 릴리스와](cloud-services-guestos-update-matrix.md)합니다.
