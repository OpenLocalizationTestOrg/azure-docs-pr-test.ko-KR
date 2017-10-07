---
title: "고객 가상 네트워크에 Azure RemoteApp 배포에 대 한 Url과 포트 toowhitelist aaaList | Microsoft Docs"
description: "포트 및 tooconfigure Azure RemoteApp을 통한 통신에 필요한 Url에 알아봅니다."
services: remoteapp
documentationcenter: 
author: mghosh1616
manager: mbaldwin
ms.assetid: 5a001ff7-14c9-47fa-9b39-78fd5a5f0250
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 039866f7b64ac763ca833d66031ade3def1d3543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="list-of-ports-and-urls-toopermit-access-for-azure-remoteapp-deployed-in-customer-virtual-network"></a>고객 가상 네트워크에에서 Azure RemoteApp 배포에 대 한 Url과 포트 toopermit 액세스 목록
> [!IMPORTANT]
> Azure RemoteApp은 2017년 8월 31일에 중단되었습니다. 읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.
> 
> 

가상 네트워크 (VNET)는 Azure RemoteApp 클라우드 또는 하이브리드 컬렉션을 배포 하는 경우 hello 다음 포트 정보를 검토 합니다. Virtual Network에 대한 자세한 내용은 [Virtual Network 개요](../virtual-network/virtual-networks-overview.md)를 참조하세요. 트래픽 toohello 가상 네트워크 리소스 컬렉션에 대 한 제한 된 네트워크 보안 그룹 NSG ()를 만든 경우 다음 포트 hello 액세스 가능 하 고 hello 가상 네트워크에 hello 보안 정책을 통해 허용 인지 확인 합니다. 네트워크 보안 그룹에 대한 자세한 내용은 다음을 참조하세요. [네트워크 보안 그룹이란? (NSG)](../virtual-network/virtual-networks-nsg.md).

## <a name="azure-remoteapp-subnet-needs-access-toothese-endpoints-and-urls"></a>Azure RemoteApp 서브넷 액세스 toothese 끝점 및 Url이 필요합니다.
* *.servicebus.windows.net
* *. servicebus.net
* https://*.remoteapp.windowsazure.com  
* https://www.remoteapp.windowsazure.com 
* https://*remoteapp.windowsazure.com  
* https://*.core.windows.net  
* 아웃바운드: TCP: TCP: 443, 9351, 9352, 10101-10175 
* 선택 사항 - UDP: 10201-10275  

## <a name="azure-remoteapp-clients-need-access-toothese-endpoints-and-urls"></a>Azure RemoteApp 클라이언트 toothese 끝점 및 Url에 액세스할 필요:
다시 말해 주는 _ 개발자 데스크톱 장치 등 hello 클라이언트에서 사용 하 여 tooconnect toohello 앱 배포 hello에 Azure RemoteApp 컬렉션.

* https://telemetry.remoteapp.windowsazure.com  
* https://*.remoteapp.windowsazure.com (이 주소는 hello 선택적 UDP 포트) 
* https://login.windows.net  
* https://login.microsoftonline.com  
* https://www.remoteapp.windowsazure.com 
* https://*.core.windows.net  
* 아웃바운드: TCP: 443  
* 선택 사항 - UDP: 3391 

