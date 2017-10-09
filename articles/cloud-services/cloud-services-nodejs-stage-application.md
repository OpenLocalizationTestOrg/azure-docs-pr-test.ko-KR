---
title: "클라우드 서비스 배포 (Node.js) aaaStage | Microsoft Docs"
description: "자세한 내용은 어떻게 toodeploy 환경을 준비 하 여 Azure 응용 프로그램 tooa 다음 스왑 VIP (가상 IP)를 사용 하 여 tooa 프로덕션 환경을 배포 합니다."
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
ms.openlocfilehash: 0656c84ac444a10f152f441265f85141347bf1fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="staging-an-application-in-azure"></a>Azure에서 응용 프로그램 준비
패키지 응용 프로그램에서 Azure toobe toohello 프로덕션 이동 하기 전에 테스트 환경을 준비 하는 배포 된 toohello 수는 hello 응용 프로그램은 hello 인터넷에서 액세스할 수 있는 환경입니다. 스테이징 환경은 hello 프로덕션 환경와 동일 하 게 액세스 hello 준비 응용 프로그램을 Azure에서 생성 하는 난독 처리 된 URL만 할 수 있습니다. 응용 프로그램이 제대로 작동 하는지 확인 한 후에 VIP (가상 IP) 교체를 수행 하 여 배포 된 toohello 프로덕션 환경 수 있습니다.

> [!NOTE]
> hello이 문서의 단계에에서만 적용 toonode 응용 프로그램을 Azure 클라우드 서비스로 호스트 됩니다.
> 
> 

## <a name="step-1-stage-an-application"></a>1단계: 응용 프로그램 스테이징
이 작업을 사용 하 여 응용 프로그램 toostage hello 하는 방법을 다룹니다 **Microsoft Azure PowerShell**합니다.

1. 서비스를 게시할 때는 hello를 전달 하면 **-슬롯** hello에 대 한 매개 변수 **게시 AzureServiceProject** cmdlet.
   
   ```powershell
   Publish-AzureServiceProject -Slot staging
   ```
2. Toohello 로그온 [Azure 클래식 포털] 선택 **클라우드 서비스**합니다. Hello 클라우드 서비스를 만들면 및 hello **준비** 너무 열 상태가 업데이트 되었으면**실행**를 hello 서비스 이름을 클릭 합니다.
   
   ![실행 중인 서비스가 표시된 포털][cloud-service]
3. 선택 hello **대시보드**를 선택한 후 **준비**합니다.
   
   ![클라우드 서비스 대시보드][cloud-service-dashboard]
4. Hello에 hello 값 확인 **사이트 URL** 항목을 오른쪽으로 toohello 합니다. hello DNS 이름은 Azure에서 생성 되는 난독 처리 된 내부 ID입니다.
   
    ![사이트 URL][cloud-service-staging-url]

이제 hello 응용 프로그램 hello 사이트 URL을 준비 하는 hello를 사용 하 여 스테이징 환경에서에서 제대로 작동 하는지 확인할 수 있습니다.

## <a name="step-2-upgrade-an-application-in-production-by-swapping-vips"></a>2단계: VIP를 교환하여 프로덕션에서 응용 프로그램 업그레이드
스테이징 환경에서 응용 프로그램의 hello 업그레이드 된 버전을 확인 한 후 있습니다 수 신속 하 게 사용할 수 있도록 프로덕션 환경에서 교체 하 여 Vip (가상 Ip) hello 스테이징 및 프로덕션 환경의 hello 합니다.

> [!NOTE]
> 이 단계는 이미 응용 프로그램 tooproduction 배포 하 고 응용 프로그램의 업그레이드 버전 hello 준비를 가정 합니다.
> 
> 

1. Hello에 로그인 [Azure 클래식 포털], 클릭 **클라우드 서비스** hello 서비스 이름을 선택 합니다.
2. Hello에서 **대시보드**을 선택 **준비**, 클릭 하 고 **교체** hello hello 페이지 맨 아래에 있습니다. Hello VIP 교체 대화가 열립니다.
   
   ![VIP 교환 대화 상자][vip-swap-dialog]
3. Hello 정보를 검토 한 다음 클릭 **확인**합니다. hello 두 개의 배포 배포 스위치 tooproduction 및 hello 프로덕션 배포 스위치 toostaging 준비 hello로 업데이트를 시작 합니다.

배포를 준비 하 고 hello 배포 준비 단계에 Vip를 교환 하 여 프로덕션 배포를 업그레이드 했습니다.

## <a name="additional-resources"></a>추가 리소스
* [어떻게 tooDeploy Azure에서 Vip를 교환 하 여 서비스 업그레이드 tooProduction]

[Azure 클래식 포털]: http://manage.windowsazure.com
[cloud-service]: ./media/cloud-services-nodejs-stage-application/staging-cloud-service-running.png
[cloud-service-dashboard]: ./media/cloud-services-nodejs-stage-application/cloud-service-dashboard-staging.png
[cloud-service-staging-url]: ./media/cloud-services-nodejs-stage-application/cloud-service-staging-url.png
[vip-swap-dialog]: ./media/cloud-services-nodejs-stage-application/vip-swap-dialog.png
[어떻게 tooDeploy Azure에서 Vip를 교환 하 여 서비스 업그레이드 tooProduction]: cloud-services-how-to-manage.md#how-to-swap-deployments-to-promote-a-staged-deployment-to-production
