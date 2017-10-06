---
title: "Azure RemoteApp과 함께 Office aaaUsing | Microsoft Docs"
description: "Office 및 Azure RemoteApp 연동 방법에 대해 알아봅니다."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: f1773baf-8aa1-423c-a2f9-e4679e0463d3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d065c1a0a2191c9e2e405264a835cecf791d6ab7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-office-with-azure-remoteapp"></a>Azure RemoteApp과 함께 Office 사용
> [!IMPORTANT]
> Azure RemoteApp은 2017년 8월 31일에 중단되었습니다. 읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.
> 
> 

Azure RemoteApp에서 Office 응용 프로그램 호스팅을 위한 두 가지 옵션으로, Office 365 ProPlus 또는 Office 2013 Professional Plus 평가판이 있습니다.

**이 문서는 향상된 새 문서로 곧 대체될 것입니다. 체크 아웃 [어떻게 toouse Azure RemoteApp과 함께 Office 365 구독](remoteapp-officesubscription.md)합니다. Office 365 + Azure RemoteApp을 사용 하기 위해 필요한 모든 hello 정보를 처리 합니다.**

## <a name="office-365-proplus"></a>Office 365 ProPlus
템플릿 이미지를 Office 365 ProPlus hello를 사용 하 여 RemoteApp 컬렉션을 만들 수 있습니다. 이 옵션 tooextend을 사용 하면 Office 365 서비스 tooRemoteApp 합니다. 기존 구독 계획에 있어야 하 고 Office 365 ProPlus 서비스를 독립 실행형 hello에 대 한 또는 hello Office 365 서비스 계획을 통해 사용자가 허가 받아야 합니다.

RemoteApp은 Office 365 공유 컴퓨터 정품 인증을 지원합니다. 공유 컴퓨터 정품 인증을 사용 하도록 설정 하 고 hello를 사용 하 여 [Office 배포 도구](http://www.microsoft.com/download/details.aspx?id=36778) 설치의 경우 Office 365 ProPlus 설치 활성화 되지 않고 있습니다. Office 365를 포함 하는 컬렉션에 사용자가 로그인 할 때 Office 365 ProPlus에 대 한 hello 사용자가 제공 하는 경우 Office toosee를 확인 합니다. 활성화 되 면, Office 일시적으로 Office 365 ProPlus-이 활성화 될 때까지 해당 사용자가 로그 아웃 hello 서비스 유지 합니다.

toouse Office 365 공유 컴퓨터 인증을 해야 toocreate는 [사용자 지정 템플릿을](remoteapp-create-custom-image.md) 및 Office 365 ProPlus 설치, 다음과 같은 [이러한 방향은](https://technet.microsoft.com/library/dn782858.aspx)합니다.

Hello에 사용자의 Office 365 라이선스를 관리할 수 있습니다 [Office 365 관리 포털](https://portal.office365.com/)합니다. [Office 365 서비스 계획](http://technet.microsoft.com/library/office-365-plan-options.aspx)에 대한 자세한 내용을 읽어 보세요.  

## <a name="office-2013-professional-plus-trial"></a>Office 2013 Professional Plus 평가판
RemoteApp의 30 일 평가판을 하는 동안 hello Office 2013 Professional 더하기 (평가판) 템플릿 이미지 toocreate RemoteApp 컬렉션을 사용할 수 있습니다. 사용자가 toothis 평가판 컬렉션 자신의 Azure Active Directory 작업 계정 또는 Microsoft 계정을 사용 하 여 할당할 수 있습니다. 추가 구독은 필요하지 않습니다.

이 가장 좋습니다 tookick hello 타이어 이며 좋은 RemoteApp에 Office 파악할 하십시오. 그러나 이 옵션은 평가 및 테스트 용도로만 사용됩니다. Hello Office 2013 Professional 더하기 (평가판) 템플릿 이미지를 사용 하 여 만든 연결 된 RemoteApp 컬렉션 모드 전환된 tooproduction 일 수 없습니다 및 hello hello 평가 기간이 끝나기 전에 수 없게 됩니다.

## <a name="switching-from-trial-tooproduction"></a>Tooproduction 평가판에서 전환
30 일 무료 평가판을 시작할 때 hello hello 포털의 RemoteApp 섹션에서에서 메모 알려 기간 남은 hello 평가판에서 유료 계정 tootransition tooa 필요 하기 전에 합니다. Hello 링크를 사용 하 여이 정보에 사용자 계정 및 스위치 tooproduction 모드를 활성화할 수 있습니다.

사용자 계정을 활성화 하면 계정에 연결 된 모든 hello RemoteApp 컬렉션이 적용 됩니다.

* Windows Server 2012 R2 hello 또는 hello Office 365 ProPlus 템플릿 이미지를 실행 중인 컬렉션 tooproduction를 원활 하 게 전환 됩니다. 진행 중인 세션을 비롯한 모든 사용자 데이터와 설정은 원래대로 유지됩니다.
* 업로드된 사용자 지정 템플릿 이미지가 있는 경우 이러한 이미지를 사용하는 컬렉션도 매끄럽게 전환됩니다.
* hello Office 2013 Professional 더하기 (평가판) 템플릿 이미지만 평가 됩니다. 이 템플릿 이미지와 실행 중인 컬렉션 전환된 tooproduction 일 수 없습니다. "사용 안 함" 상태로 설정됩니다.

평가판의 만료 hello로 tooproduction 모드를 전환 되지 않으면 RemoteApp 컬렉션 비활성화 됩니다. 걱정 하지 마십시오-설정 및 사용자 데이터 저장 되므로 다른 90 일 동안 데이터 손실 없이 사용자 서비스 및 스위치 tooproduction 모드를 활성화할 수 있습니다.

