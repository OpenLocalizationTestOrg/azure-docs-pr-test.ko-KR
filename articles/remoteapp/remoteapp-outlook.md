---
title: "Azure RemoteApp에서 Outlook aaaUsing | Microsoft Docs"
description: "자세한 내용은 방법 tooconfigure Outlook을 사용 하 여 Azure RemoteApp에서 | Microsoft Azure"
services: remoteapp
documentationcenter: 
author: pavithir
manager: mbaldwin
ms.assetid: cb2a498f-9539-4522-a874-542114926a61
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 119d2629ac47bd8d20d617985a9b488068aa959f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-microsoft-outlook-in-azure-remoteapp"></a>Azure RemoteApp에서 Microsoft Outlook 사용
> [!IMPORTANT]
> Azure RemoteApp은 2017년 8월 31일에 중단되었습니다. 읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.
> 
> 

Azure RemoteApp은 Microsoft Outlook O365를 지원합니다. [Azure RemoteApp에서 Office가 작동하는 방식](remoteapp-officesubscription.md)에 대해 자세히 알아보세요. Azure RemoteApp에서 사용하는 경우 Outlook에 대한 몇 가지 권장되는 설정이 있습니다.

## <a name="cached-mode"></a>캐시 모드
캐시 모드는 Azure RemoteApp에서 Outlook을 사용할 때 권장되는 구성입니다. 캐시 된 Exchange 모드를 Outlook 2013 hello 오프 라인 주소록 함께 hello 사용자의 컴퓨터에서 오프 라인 데이터 파일 (OST 파일)에 저장 된 hello 사용자의 Microsoft Exchange 사서함의 로컬 복사본에서 작동 하는 Outlook 2013 계정 toouse를 구성 하는 경우 OAB ()입니다. 캐시 된 사서함 hello 및 OAB hello O365 서비스에서에서 정기적으로 업데이트 됩니다. 에 대해 자세히 알아보세요 [캐시 및 온라인 모드 간 차이점 hello](https://technet.microsoft.com/library/jj683103.aspx)합니다.

hello 선택할 수 있는 **Exchange 캐시 된 모드** 또는 **온라인 모드** 계정 설정 되어 있거나 hello 계정 설정을 변경 하 여 합니다. 또한 하나의 모드 또는 다른 hello hello Office 사용자 지정 도구 (OCT) 이나 그룹 정책을 사용 하 여 배포할 수 있습니다.  

[캐시 모드를 활성화하는 단계별 지침](https://technet.microsoft.com/library/c6f4cad9-c918-420e-bab3-8b49e1885034#proc)을 확인하세요.

## <a name="search"></a>검색
Azure RemoteApp에서 Outlook 내의 검색을 사용하는 데는 제한 사항이 있습니다. Azure RemoteApp 풀링된 Vm tooaccommodate 사용자 세션을 사용합니다. 검색 인덱싱 다른 Vm에 대 한 다른 hello 컴퓨터 ID에 따라 달라 집니다. 사용자가 Azure RemoteApp에는 로그인, 때마다는 방향이 지정 된 tooa 수 새 VM입니다. 메시지의 의미는 로컬 검색을 사용 하도록 설정 하는 경우 hello 인덱서 hello 컴퓨터 ID (hello 사용자가 다른 VM에도) 하는 경우이 변경 될 때마다 실행 됩니다. Hello의 hello 크기에 따라. OST hello 인덱서 수 오랜 시간이 toocomplete 걸릴 파일과 다른 앱에 필요한 리소스를 사용 합니다. 검색 속도도 느리고 결과가 생성되지 않을 수도 있습니다. 로컬 캐시의 toohello 부족 때문이 전반적인 성능이 저하 될 수 있지만 온라인 모드 계정 프로필을 사용 하 여이 문제를 해결 작동할 것 (캐시 된 및 온라인 모드의 hello 차이점에 대 한 자세한 내용은 위에 링크 hello 참조). 아쉽게도 Outlook 2013에서는 기본적으로 인덱싱된/로컬 검색을 비활성화할 수 없으며 온라인 검색을 활성화할 수 없습니다.

