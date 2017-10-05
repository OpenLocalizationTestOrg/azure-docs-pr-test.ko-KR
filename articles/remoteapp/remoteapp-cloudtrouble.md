---
title: "RemoteApp 클라우드 컬렉션 - 만들기 문제 해결 | Microsoft Docs"
description: "RemoteApp 클라우드 컬렉션 만들기 오류 문제를 해결하는 방법을 알아봅니다."
services: remoteapp
documentationcenter: 
author: vkbucha
manager: mbaldwin
ms.assetid: 95eb7797-7b5e-4781-ad23-f15dd85b213d
ms.service: remoteapp
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 304ba7c5057b27c459bccbb75d3a711567757675
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-creating-remoteapp-cloud-collections"></a>RemoteApp 클라우드 컬렉션 만들기 문제 해결
> [!IMPORTANT]
> Azure RemoteApp은 2017년 8월 31일에 중단되었습니다. 자세한 내용은 [알림](https://go.microsoft.com/fwlink/?linkid=821148) 을 읽어보세요.
> 
> 

클라우드 컬렉션을 만드는 데 문제가 있는 경우 다음 정보를 확인합니다.

## <a name="your-image-is-invalid"></a>이미지가 올바르지 않음
Azure의 컬렉션 프로비전을 대기하는 중에 "GoldImageInvalid" 등의 메시지가 나타나면 템플릿 이미지가 [정의된 이미지 요구 사항](remoteapp-imagereqs.md)에 부합하지 않음을 나타냅니다. 따라서 해당 [요구 사항](remoteapp-imagereqs.md)을 읽고 이미지를 수정한 다음 다시 컬렉션을 만듭니다.

## <a name="common-errors-seen-in-the-azure-management-portal"></a>Azure 관리 포털에 표시되는 일반적인 오류
    DNS server could not be reached
    ProvisioningTimeout

사용자 지정 이미지를 사용하기 때문에 만들기 중 클라우드 컬렉션이 자주 실패합니다.  위의 오류 중 하나를 참조하고 사용자 지정 이미지를 사용하여 컬렉션을 만드는 경우, 다음과 같은 작업을 확인하십시오.

* 업로드한 사용자 지정 이미지가 이미지 요구 사항을 만족하는지 확인합니다.
* 가장 자주 발생하는 일반적인 문제는 이미지가 제대로 sysprep되지 않은 것입니다.  
* 이미지를 Hyper-V 내에서 부팅할 수 있는지 확인하고 이미지를 사용하여 Azure 구독에서 직접 IAAS VM을 만듭니다. VM을 부팅하고 시작할 수 없는 경우, 다음은 일반적으로 사용자 지정 이미지가 올바르게 준비되지 않았음을 나타냅니다.  RemoteApp에 대한 사용자 지정 템플릿 이미지를 만드는 방법에 따라 사용자 지정 이미지가 빌드되었는지 확인합니다.

구독에 포함된 Microsoft 이미지 중 하나를 사용하는 경우, 컬렉션을 다시 만듭니다. 문제가 지속되면 다음 Microsoft 지원에 문의하세요.

    PlatformImageTrialModeOnly

이 오류가 발생한 경우, 일반적으로 유료 계정으로 업그레이드되었음을 의미하지만 서비스의 평가 모드 중에만 유효한 Microsoft 제공 이미지를 사용하려고 함을 의미합니다. 이 경우, 다시 클라우드 컬렉션을 만들어 보지만 올바른 이미지를 지정해야 합니다.

