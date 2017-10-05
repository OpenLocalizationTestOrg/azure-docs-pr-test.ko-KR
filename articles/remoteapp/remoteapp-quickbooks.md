---
title: "Azure RemoteApp에서 QuickBooks 배포 | Microsoft 문서"
description: "Azure RemoteApp과 QuickBooks 공유 방법을 알아봅니다."
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: c5d00753-77c0-4f0d-a5df-9451b46a31d3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: bbfac45220f6ef36c9951daae0ced1974e8ddabb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-do-you-deploy-quickbooks-in-azure-remoteapp"></a>Azure RemoteApp에서 QuickBooks를 배포하려면 어떻게 해야 할까요?
> [!IMPORTANT]
> Azure RemoteApp은 2017년 8월 31일에 중단되었습니다. 자세한 내용은 [알림](https://go.microsoft.com/fwlink/?linkid=821148) 을 읽어보세요.
> 
> 

다음 정보를 사용하여 Azure RemoteApp에서 QuickBooks를 앱으로 공유할 수 있습니다.

하이브리드 또는 클라우드 컬렉션에 QuickBooks 2015 Enterprise를 Azure remoteapp과 공유할 수 있습니다. 회사 파일은 Azure RemoteApp 서버와 별개의 QuickBooks 데이터베이스 서버를 실행 중인 VM에 있어야 합니다. Azure RemoteApp 이미지에 회사 파일을 저장하지 마십시오. - 이렇게 하면 데이터 손실이 예상됩니다. QuickBooks Enterprise만 표준 Windows 네트워킹을 통해 액세스할 수 있는 QuickBooks 데이터베이스 서버와 외부 공유에 대한 QuickBooks 파일 호스팅을 지원합니다.   

> [!IMPORTANT]
> 회사 파일을 호스팅하는 QuickBooks 데이터베이스 서버는 Azure RemoteApp 컬렉션과 동일한 VNET 내의 별도 VM에 있어야 합니다.  
> 
> 

## <a name="steps-to-deploy-quickbooks"></a>QuickBooks를 배포하는 단계
1. Azure VM을 만들고 QuickBooks, QuickBooks 데이터베이스 서버를 설치하고 Azure VM에 회사 파일을 저장합니다.  방화벽 규칙을 올바르게 구성해야 합니다.
2. 회사 파일이 있는 QuickBooks 데이터베이스 서버를 호스팅하는 VM이 있는 위치와 똑같은 VNET 내에서 [ 사용자 지정 이미지 ](remoteapp-imageoptions.md)에 QuickBooks를 설치하고 [Azure RemoteApp 컬렉션](remoteapp-collections.md)(클라우드 또는 하이브리드)을 만듭니다. 
3. [게시](remoteapp-publish.md) 
4. Azure RemoteApp이 호스팅하는 QuickBooks 클라이언트를 시작하고, 표준 Windows 네트워킹을 사용하여 QuickBooks 데이터베이스 서버를 호스팅하는 VM으로 이동하고, 회사 파일을 엽니다. 

## <a name="documentation-references"></a>설명서 참조
* QuickBooks [지원되는 구성](http://enterprisesuite.intuit.com/products/enterprise-solutions/technical/#top)
* QuickBooks [배포 옵션](http://enterprisesuite.intuit.com/everythingenterprise/launchpad/new-user/)

또한 필자의 Ignite 프레젠테이션인 [Microsoft Azure RemoteApp 관리 기초](https://channel9.msdn.com/Events/Ignite/2015/BRK3868)를 살펴볼 수도 있습니다. QuickBooks 부분에 도달하려면 1:02:45 지점까지 빨리 감으세요.

## <a name="deployment-architecture"></a>배포 아키텍처
![QuickBooks + Azure RemoteApp 배포](./media/remoteapp-quickbooks/ra-quickbooks.png)

