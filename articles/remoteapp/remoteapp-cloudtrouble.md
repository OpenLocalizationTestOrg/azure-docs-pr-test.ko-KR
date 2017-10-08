---
title: "aaaTroubleshoot RemoteApp 클라우드 컬렉션 만들기 | Microsoft Docs"
description: "Tootroubleshoot RemoteApp 컬렉션 만들기 실패 클라우드 하는 방법에 대해 알아봅니다"
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
ms.openlocfilehash: 9484ecbdb048ede8df725215b313e049cc7648f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-creating-remoteapp-cloud-collections"></a>RemoteApp 클라우드 컬렉션 만들기 문제 해결
> [!IMPORTANT]
> Azure RemoteApp은 2017년 8월 31일에 중단되었습니다. 읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.
> 
> 

클라우드 컬렉션을 만드는 하는 데 문제가 hello 다음 정보를 확인 합니다.

## <a name="your-image-is-invalid"></a>이미지가 올바르지 않음
컬렉션에 대 한 Azure tooprovision 대기 중인 때 "GoldImageInvalid" 같은 메시지가 나타나면 템플릿 이미지 hello를 충족 하지 않는 것 [이미지 요구 사항 정의](remoteapp-imagereqs.md)합니다. 따라서 읽을 것을 이동 [요구 사항](remoteapp-imagereqs.md), 이미지를 수정 및 toocreate 컬렉션을 다시 시도 하십시오.

## <a name="common-errors-seen-in-hello-azure-management-portal"></a>Hello Azure 관리 포털에서 표시 하는 일반적인 오류
    DNS server could not be reached
    ProvisioningTimeout

사용자 지정 이미지를 사용하기 때문에 만들기 중 클라우드 컬렉션이 자주 실패합니다.  오류가 위에 hello 중 하나를 참조 하는 경우 사용자 지정 이미지 toocreate hello 컬렉션을 사용 하는 작업을 수행 하는 hello를 참조 하세요.

* Hello 사용자 지정 이미지 업로드 한 이미지 요구 사항을 충족 하는지 확인 합니다.
* Hello 일반적인 문제 가장 자주 hello 이미지가 올바르게 되지 않았습니다 syspreped입니다.  
* 확인 hello 이미지 Hyper-v 내에서 부팅 하거나 hello 이미지를 사용 하 여 Azure 구독에서 직접 IAAS VM을 만들어 보십시오. Hello VM tooboot 및 시작 하지 못하면 다음 일반적으로이 나타냅니다 hello 사용자 지정 이미지가 제대로 준비 되지 않았습니다.  사용자 지정 이미지가 hello 어떻게 toocreate 사용자 지정 서식 파일의 이미지 RemoteApp hello 다음 빌드 되었는지 확인

구독에 포함 된 hello Microsoft 이미지 중 하나를 사용 하는 경우에 toocreate hello 컬렉션을 다시 시도 하십시오. Hello 문제가 계속 되 면 다음 Microsoft 지원을 요청 하십시오.

    PlatformImageTrialModeOnly

이 오류를 참조 하는 경우이 일반적으로 의미 업그레이드 된 tooa 계정 지만 toouse hello hello 서비스의 평가 모드 중에 유효 하는 Microsoft에서 제공 이미지를 시도 합니다. 이 경우 toocreate 하면 클라우드 컬렉션을 다시 시도 하십시오 되지만 있는지 toospecify hello 올바른 이미지 여야 합니다.

