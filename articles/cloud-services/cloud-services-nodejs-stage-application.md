---
title: "클라우드 서비스 배포 준비(Node.js) | Microsoft Docs"
description: "Azure 응용 프로그램을 스테이징 환경에 배포한 다음 VIP(가상 IP) 교환을 사용하여 프로덕션 환경에 배포하는 방법에 대해 알아봅니다."
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: d65d26a6-b424-49cd-a88c-7ef46bb112a8
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: b3000ed769e8c60eccb21e26f53ce7ccb7e68d7f
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/11/2017
---
# <a name="staging-an-application-in-azure"></a>Azure에서 응용 프로그램 준비
패키지 응용 프로그램을 먼저 Azure의 스테이징 환경에 배포하여 테스트한 후 해당 응용 프로그램을 인터넷에서 액세스할 수 있는 프로덕션 환경으로 이동할 수 있습니다. 스테이징 환경은 Azure에서 생성하는 숨겨진 URL로 미리 구성된 응용 프로그램에만 액세스할 수 있다는 점을 제외하면 프로덕션 환경과 똑같습니다. 응용 프로그램이 올바르게 작동되는지 확인한 후 VIP(가상 IP) 교환을 수행하여 해당 응용 프로그램을 프로덕션 환경으로 배포할 수 있습니다.

> [!NOTE]
> 이 문서의 단계는 Azure 클라우드 서비스로 호스트되는 노드 응용 프로그램에만 적용됩니다.
> 
> 

## <a name="step-1-stage-an-application"></a>1단계: 응용 프로그램 스테이징
이 작업은 **Microsoft Azure PowerShell**을 사용하여 응용 프로그램을 준비하는 방법에 대해 다룹니다.

1. 서비스를 게시할 때 단지 **-Slot** 매개 변수를 **Publish-AzureServiceProject** cmdlet으로 전달합니다.
   
   ```powershell
   Publish-AzureServiceProject -Slot staging
   ```
2. [Azure 클래식 포털] 에 로그온하고 **클라우드 서비스**를 선택합니다. 클라우드 서비스가 만들어지고 **스테이징** 열 상태가 **실행 중**으로 업데이트된 후 서비스 이름을 클릭합니다.
   
   ![실행 중인 서비스가 표시된 포털][cloud-service]
3. **대시보드**를 선택한 후 **스테이징**을 선택합니다.
   
   ![클라우드 서비스 대시보드][cloud-service-dashboard]
4. 오른쪽에 있는 **사이트 URL** 항목의 값을 기록합니다. DNS 이름은 Azure에서 생성한 임시 내부 ID입니다.
   
    ![사이트 URL][cloud-service-staging-url]

이제 응용 프로그램이 스테이징 사이트 URL을 사용하여 스테이징 환경에서 올바르게 작동하고 있는 것을 확인할 수 있습니다.

## <a name="step-2-upgrade-an-application-in-production-by-swapping-vips"></a>2단계: VIP를 교환하여 프로덕션에서 응용 프로그램 업그레이드
스테이징 환경에서 업그레이드된 버전의 응용 프로그램을 확인한 후 스테이징 환경과 프로덕션 환경의 VIP(가상 IP)를 교환하여 프로덕션에서 해당 응용 프로그램을 빠르게 사용하도록 설정할 수 있습니다.

> [!NOTE]
> 이 단계에서는 프로덕션에 응용 프로그램을 이미 배포했으며 업그레이드된 버전의 응용 프로그램을 미리 구성했다고 가정합니다.
> 
> 

1. [Azure 클래식 포털]에 로그인하고 **클라우드 서비스** 를 클릭한 후 서비스 이름을 선택합니다.
2. **대시보드**에서 **스테이징**을 선택한 후 페이지 맨 아래에 있는 **교환**을 클릭합니다. 그러면 VIP 교환 대화 상자가 열립니다.
   
   ![VIP 교환 대화 상자][vip-swap-dialog]
3. 정보를 검토한 후 **확인**을 클릭합니다. 스테이징 배포가 프로덕션으로, 프로덕션 배포가 스테이징으로 전환되면서 두 배포가 업데이트를 시작합니다.

배포를 미리 구성하고, 스테이징의 배포와 VIP를 교환하여 프로덕션 배포를 업그레이드했습니다.

## <a name="additional-resources"></a>추가 리소스
* [Azure에서 VIP를 교환하여 프로덕션에 서비스 업그레이드를 배포하는 방법]

[Azure 클래식 포털]: http://manage.windowsazure.com
[cloud-service]: ./media/cloud-services-nodejs-stage-application/staging-cloud-service-running.png
[cloud-service-dashboard]: ./media/cloud-services-nodejs-stage-application/cloud-service-dashboard-staging.png
[cloud-service-staging-url]: ./media/cloud-services-nodejs-stage-application/cloud-service-staging-url.png
[vip-swap-dialog]: ./media/cloud-services-nodejs-stage-application/vip-swap-dialog.png
[Azure에서 VIP를 교환하여 프로덕션에 서비스 업그레이드를 배포하는 방법]: cloud-services-how-to-manage.md#how-to-swap-deployments-to-promote-a-staged-deployment-to-production
