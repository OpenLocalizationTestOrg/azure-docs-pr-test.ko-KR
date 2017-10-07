---
title: "Azure에서 앱을 aaaScale | Microsoft Docs"
description: "자세한 방법을 tooscale Azure 앱 서비스 tooadd 용량 및 기능에 앱을 합니다."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: f7091b25-b2b6-48da-8d4a-dcf9b7baccab
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2016
ms.author: cephalin
ms.openlocfilehash: 97f46f77aeef95aec90d38e8396a023820e3caeb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-up-an-app-in-azure"></a>Azure에서 앱 강화
이 문서에서는 어떻게 tooscale Azure 앱 서비스에서 응용 프로그램입니다. 크기 조정, 눈금에 대 한 두 개의 워크플로를 있으며 규모를 확장 하 고이 문서에서는 워크플로를 hello 눈금에 설명 합니다.

* [강화](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): 더 많은 CPU, 메모리, 디스크 공간 및 추가 기능(전용 가상 컴퓨터(VM), 사용자 지정 도메인 및 인증서, 스테이징 슬롯, 자동 크기 조정 등)을 사용할 수 있습니다. 가격 책정 계층에 속하는 응용 프로그램은 앱 서비스 계획의 hello를 변경 하 여 확장 합니다.
* [확장할](https://en.wikipedia.org/wiki/Scalability#Horizontal_and_vertical_scaling): hello 응용 프로그램을 실행 하는 VM 인스턴스 수를 증가 합니다.
  수평 확장할 수 있습니다 tooas 20 인스턴스로 여러 가격 책정 계층에 따라 합니다. [앱 서비스 환경](../app-service/app-service-app-service-environments-readme.md) 에 **프리미엄** 계층 확장 개수 too50 인스턴스를 더욱 높일 됩니다. 규모 확장에 대한 자세한 내용은 [수동 또는 자동으로 인스턴스 개수 조정](../monitoring-and-diagnostics/insights-how-to-scale.md)을 참조하세요. 알 수 없는 아웃 tooscale 인스턴스 개수를 자동으로 인 한 toouse 자동 크기 조정 미리 정의 된 규칙 및 일정에 따라 하는 방법입니다.

크기 조정 설정을 take만 초 tooapply hello 및에서 모든 앱에 영향을 줄 사용자 [앱 서비스 계획](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)합니다.
필요 하면 toochange 코드 또는 응용 프로그램을 다시 배포 하지 않습니다.

개별 앱 서비스 계획의 hello 가격 및 기능에 대 한 정보를 참조 하십시오. [앱 서비스 가격 정보](https://azure.microsoft.com/pricing/details/web-sites/)합니다.  

> [!NOTE]
> 앱 서비스 계획 hello에서 전환 하기 전에 **무료** 계층 hello를 먼저 제거 해야 [지출 한도](https://azure.microsoft.com/pricing/spending-limits/) Azure 구독에 대 한 위치에. Microsoft Azure 앱 서비스 구독에 대 한 tooview 또는 변경 옵션 참조 [Microsoft Azure 구독][azuresubscriptions]합니다.
> 
> 

<a name="scalingsharedorbasic"></a>
<a name="scalingstandard"></a>

## <a name="scale-up-your-pricing-tier"></a>가격 책정 계층 강화
1. 브라우저를 열고 hello [Azure 포털][portal]합니다.
2. 앱 블레이드에서 **모든 설정**을 클릭한 다음 **강화**를 클릭합니다.
   
    ![Azure 앱을 tooscale를 이동 합니다.][ChooseWHP]
3. 사용자 계층을 선택한 다음 **선택**을 클릭합니다.
   
    hello **알림** 탭 녹색 깜박입니다 **성공** hello 작업이 완료 된 후입니다.

<a name="ScalingSQLServer"></a>

## <a name="scale-related-resources"></a>규모 관련 리소스
앱이 Azure SQL 데이터베이스 또는 Azure 저장소와 같은 다른 서비스에 종속된 경우 요구에 따라 해당 리소스를 강화할 수도 있습니다. 이러한 리소스 앱 서비스 계획 hello로 배율이 조정 되지 않으므로 별도로 배율을 조정 해야 합니다.

1. **Essentials**, hello 클릭 **리소스 그룹** 링크 합니다.
   
    ![Azure 앱의 관련 리소스를 강화합니다.](./media/web-sites-scale/RGEssentialsLink.png)
2. Hello에 **요약** hello의 일부가 **리소스 그룹** 블레이드에서 tooscale 리소스 클릭 합니다. 다음 스크린 샷 hello Azure 저장소 리소스 및 SQL 데이터베이스 리소스를 보여 줍니다.
   
    ![Azure 앱을 tooresource 그룹 블레이드 tooscale 이동](./media/web-sites-scale/ResourceGroup.png)
3. SQL 데이터베이스 리소스에 대 한 클릭 **설정** > **가격 책정 계층** tooscale hello 가격 책정 계층입니다.
   
    ![Azure 앱에 대 한 hello SQL 데이터베이스 백 엔드가 수직 확장](./media/web-sites-scale/ScaleDatabase.png)
   
    또한 SQL 데이터베이스 인스턴스에 [지역에서 복제](../sql-database/sql-database-geo-replication-overview.md) 를 설정합니다.
   
    Azure 저장소 리소스에 대 한 클릭 **설정** > **구성** tooscale 저장소 옵션입니다.
   
    ![Azure 응용 프로그램에서 사용 하는 hello Azure 저장소 계정 수직 확장](./media/web-sites-scale/ScaleStorage.png)

<a name="devfeatures"></a>

## <a name="learn-about-developer-features"></a>개발자 기능에 대해 알아보기
따라 hello 가격 책정 계층, hello 다음 개발자 중심 기능을 사용할 수 있습니다.

### <a name="bitness"></a>비트 수
* hello **기본**, **표준**, 및 **프리미엄** 계층 64 비트 및 32 비트 응용 프로그램을 지원 합니다.
* hello **무료** 및 **Shared** 계획 계층 32 비트 응용 프로그램의 경우에 지원 합니다.

### <a name="debugger-support"></a>디버거 지원
* Hello에 대 한 디버거 지원 됩니다. **무료**, **Shared**, 및 **기본** 앱 서비스 계획 당 연결이 하나에 모드입니다.
* Hello에 대 한 디버거 지원 됩니다. **표준** 및 **프리미엄** 앱 서비스 계획 당 5 개의 동시 연결 수에 모드입니다.

<a name="OtherFeatures"></a>

## <a name="learn-about-other-features"></a>다른 기능에 대해 알아보기
* 모든 hello 남은 hello 앱 서비스의에서 기능에 대 한 자세한 내용은 가격 책정 등의 계획 및 관심 있는 tooall 사용자 (개발자 포함)의 기능 참조 [앱 서비스 가격 정보](https://azure.microsoft.com/pricing/details/web-sites/)합니다.

> [!NOTE]
> Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](https://azure.microsoft.com/try/app-service/) 앱 서비스의 수명이 짧은 스타터 웹 응용 프로그램 즉시 만들 수 있는 합니다. 신용 카드는 필요하지 않으며 약정은 없습니다.
> 
> 

<a name="Next Steps"></a>

## <a name="next-steps"></a>다음 단계
* azure를 시작 하는 tooget 참조 [Microsoft Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)합니다.
* 가격, 지원 및 SLA에 대 한 내용은 hello 다음 링크를 방문 합니다.
  
    [데이터 전송 가격 정보](https://azure.microsoft.com/pricing/details/data-transfers/)
  
    [Microsoft Azure 지원 계획](https://azure.microsoft.com/support/plans/)
  
    [서비스 수준 계약](https://azure.microsoft.com/support/legal/sla/)
  
    [SQL 데이터베이스 가격 정보](https://azure.microsoft.com/pricing/details/sql-database/)
  
    [Microsoft Azure를 위한 가상 컴퓨터 및 클라우드 서비스 크기][vmsizes]
  
    [앱 서비스 가격 정보](https://azure.microsoft.com/pricing/details/app-service/)
  
    [앱 서비스 가격 정보 - SSL 연결](https://azure.microsoft.com/pricing/details/web-sites/#ssl-connections)
* 확장성 있고 복원력이 뛰어난 아키텍처 빌드를 포함하여 Azure 앱 서비스 모범 사례에 대한 자세한 내용은 [모범 사례: Azure 앱 서비스 웹앱](http://blogs.msdn.com/b/windowsazure/archive/2014/02/10/best-practices-windows-azure-websites-waws.aspx)을 참조하세요.
* 앱 서비스 앱 크기 조정 하는 방법에 대 한 동영상 hello 다음 리소스를 참조 하십시오.
  
  * [때 tooScale Stefan Schackow와 Azure 웹 사이트-](https://azure.microsoft.com/resources/videos/azure-web-sites-free-vs-standard-scaling/)
  * [Azure 웹 사이트, CPU 또는 예약 리소스 크기 자동 조정 - 스테판 스차코우(Stefan Schackow)](https://azure.microsoft.com/resources/videos/auto-scaling-azure-web-sites/)
  * [Azure 웹 사이트 크기 조정 방법 - 스테판 스차코우(Stefan Schackow)](https://azure.microsoft.com/resources/videos/how-azure-web-sites-scale/)

<!-- LINKS -->
[vmsizes]:/pricing/details/app-service/
[SQLaccountsbilling]:http://go.microsoft.com/fwlink/?LinkId=234930
[azuresubscriptions]:http://go.microsoft.com/fwlink/?LinkID=235288
[portal]: https://portal.azure.com/

<!-- IMAGES -->
[ChooseWHP]: ./media/web-sites-scale/scale1ChooseWHP.png
[ChooseBasicInstances]: ./media/web-sites-scale/scale2InstancesBasic.png
[SaveButton]: ./media/web-sites-scale/05SaveButton.png
[BasicComplete]: ./media/web-sites-scale/06BasicComplete.png
[ScaleStandard]: ./media/web-sites-scale/scale3InstancesStandard.png
[Autoscale]: ./media/web-sites-scale/scale4AutoScale.png
[SetTargetMetrics]: ./media/web-sites-scale/scale5AutoScaleTargetMetrics.png
[SetFirstRule]: ./media/web-sites-scale/scale6AutoScaleFirstRule.png
[SetSecondRule]: ./media/web-sites-scale/scale7AutoScaleSecondRule.png
[SetThirdRule]: ./media/web-sites-scale/scale8AutoScaleThirdRule.png
[SetRulesFinal]: ./media/web-sites-scale/scale9AutoScaleFinal.png
[ResourceGroup]: ./media/web-sites-scale/scale10ResourceGroup.png
[ScaleDatabase]: ./media/web-sites-scale/scale11SQLScale.png
[GeoReplication]: ./media/web-sites-scale/scale12SQLGeoReplication.png
