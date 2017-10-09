---
title: "RemoteApp VNET tooan Azure VNET에서에서 aaaHow toomigrate | Microsoft Docs"
description: "자세한 방법을 toomigrate RemoteApp VNET tooan Azure VNET에서"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: baea5d29-353b-48f8-b47f-806f2163e067
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: c0f8617556c6f1e33eca8322febf67ff33937ecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomigrate-a-hybrid-collection-from-a-remoteapp-vnet-tooan-azure-vnet"></a>어떻게 toomigrate RemoteApp VNET tooan Azure VNET에서에서 하이브리드 컬렉션
> [!IMPORTANT]
> Azure RemoteApp은 2017년 8월 31일에 중단되었습니다. 읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.
> 
> 

기쁘게도 기존 Azure 가상 네트워크 (Vnet) 관련 RemoteApp Vnet을 만드는 대신에 직접 연결 된 하이브리드 RemoteApp 컬렉션 toodeploy 설정한 합니다. 이렇게 하면 hello (예: ExpressRoute) 최신 VNET 기능을 이용 하 고 프로그램 하이브리드 컬렉션 네트워크에 직접 액세스 tooother Azure 서비스를 제공 하 고 가상 컴퓨터 배포 toothat VNET 키를 누릅니다.  따라서 VNET 간 구성보다 성능이 더 우수하고 더 쉽게 설정할 수 있습니다.

*OriginalCollection*이라는 하이브리드 RemoteApp 컬렉션과 *RemoteAppVNET*이라는 RemoteApp VNET을 이미 만들었다고 가정합니다. 다음 hello 단계 toomigrate은 것 새 Azure VNET 이라는 tooa *AzureVNET*합니다.

1. Hello에 **네트워크** hello 탭 [관리 포털](http://manage.windowsazure.com/), 호출 VNET을 만들 *AzureVNET*를 사용 하 여 하나 이상의 (에 동일한 위치, DNS 구성 및 주소 공간 hello hello *AzureVNET* 서브넷)에 사용한 *RemoteAppVNET*합니다.
2. 구성 *AzureVNET* tooeither 호스트 하거나 네트워크 연결 toohello Active Directory 배포는 *OriginalCollection* 에 도메인 가입 되어 있습니다.
3. Hello에 **Remoteapp** 탭에서 이라는 새 RemoteApp 컬렉션을 만들 *새 컬렉션*합니다. (사용 하 여 hello **VNET와 함께 만들기** 옵션 하지 **빠른 생성**.)
4. 구성 *NewCollection* toobe tooa 서브넷에 배포 된 *AzureVNET*합니다.
5. 구성 *NewCollection* toouse hello 같은 이미지와 도메인 가입 정보에 사용한 *OriginalCollection*합니다.
6. 몇 시간 후 *NewCollection* 이 컬렉션 목록에 활성 상태로 표시됩니다.

이제 toomigrate hello 원래 컬렉션 toohello 새 컬렉션에서 어떤 사용자 정보도 필요 없는 경우 다음이 단계를 수행 다음:

1. *OriginalCollection*을 삭제합니다.
2. *RemoteAppVNET*을 삭제합니다.

완료되었습니다!

또는 hello 원래 컬렉션 toohello 새 컬렉션에서 toomigrate 사용자 정보를 해야 하는 경우 다음이 단계를 수행 다음:

1. 너무 전자 메일을 보내[ remoteappforum@microsoft.com ](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20user%20information%20migration) 를 Azure 구독 ID로, 원래 컬렉션의 이름 및 새 컬렉션의 hello 이름을 hello 것을 요청 toomigrate 사용자 정보입니다.
2. 업무일 기준 2 일 내 hello a p p 팀이 hello 사용자 액세스 목록 및 모든 사용자 문서 및 사용자 설정 hello 원래 컬렉션 toohello 새 컬렉션에서 이동 합니다.
3. *OriginalCollection*을 삭제합니다.
4. *RemoteAppVNET*을 삭제합니다.

완료되었습니다!

궁금한 사항이 있거나 특별한 지원이 필요한 경우 [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20VNET%20migration%20help)이라는 RemoteApp VNET을 이미 만들었다고 가정합니다.

