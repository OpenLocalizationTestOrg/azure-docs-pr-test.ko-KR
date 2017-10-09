---
title: "Azure RemoteApp에서 QuickBooks aaaDeploy | Microsoft Docs"
description: "자세한 내용은 방법 tooshare QuickBooks Azure RemoteApp과 함께 합니다."
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
ms.openlocfilehash: c21b1ac311449be2281f9ce157828260e856f55d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-do-you-deploy-quickbooks-in-azure-remoteapp"></a>Azure RemoteApp에서 QuickBooks를 배포하려면 어떻게 해야 할까요?
> [!IMPORTANT]
> Azure RemoteApp은 2017년 8월 31일에 중단되었습니다. 읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.
> 
> 

Azure RemoteApp에서 응용 프로그램으로 정보 tooshare QuickBooks 다음 hello를 사용 합니다.

하이브리드 또는 클라우드 컬렉션에 QuickBooks 2015 Enterprise를 Azure remoteapp과 공유할 수 있습니다. hello 회사 파일 hello Azure RemoteApp 서버와에서 별개인 QuickBooks 데이터베이스 서버를 실행 하는 VM에 있어야 합니다. Azure RemoteApp 이미지에 hello 회사 파일을 저장 하지 않으며-이 작업을 수행 하는 경우 데이터 손실이 사용할 수 있습니다. QuickBooks 엔터프라이즈만 표준 Windows 네트워킹을 통해 액세스할 수 있는 QuickBooks 데이터베이스 서버와 외부 공유에 호스팅 hello QuickBooks 파일을 지원합니다.   

> [!IMPORTANT]
> hello hello 회사 파일을 호스팅하는 QuickBooks 데이터베이스 서버에 있어야 hello 내에서 별도 VM 동일한 VNET hello Azure RemoteApp 컬렉션으로.  
> 
> 

## <a name="steps-toodeploy-quickbooks"></a>단계 toodeploy QuickBooks
1. Azure VM 만들기 QuickBooks, QuickBooks 데이터베이스 서버와 Azure VM에 hello 회사 파일을 배치 합니다.  방화벽 규칙을 구성 하는지 tooproperly를 확인 합니다.
2. 에 QuickBooks 설치는 [사용자 지정 이미지](remoteapp-imageoptions.md) 만듭니다는 [Azure RemoteApp 컬렉션](remoteapp-collections.md), 클라우드 또는 하이브리드 hello 내에서 정확히 동일한 VNET 위치와 데이터베이스 서버를 QuickBooks hello hello VM 호스팅 회사 파일에 상주 합니다. 
3. [게시](remoteapp-publish.md) QuickBooks 앱 toousers
4. Hello Azure RemoteApp 호스팅되지 QuickBooks 클라이언트를 시작 하 고 표준 Windows 네트워킹 toohello VM 호스팅 hello QuickBooks 데이터베이스 서버를 사용 하 여 탐색 hello 회사 파일을 엽니다. 

## <a name="documentation-references"></a>설명서 참조
* QuickBooks [지원되는 구성](http://enterprisesuite.intuit.com/products/enterprise-solutions/technical/#top)
* QuickBooks [배포 옵션](http://enterprisesuite.intuit.com/everythingenterprise/launchpad/new-user/)

Ignite 프레젠테이션을 확인할 수 있습니다 [Microsoft Azure RemoteApp 관리 기본 사항 및 관리](https://channel9.msdn.com/Events/Ignite/2015/BRK3868) -too1:02:45 tooget toohello QuickBooks 부분 빨리 감기 합니다.

## <a name="deployment-architecture"></a>배포 아키텍처
![QuickBooks + Azure RemoteApp 배포](./media/remoteapp-quickbooks/ra-quickbooks.png)

