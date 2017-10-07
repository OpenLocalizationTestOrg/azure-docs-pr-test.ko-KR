---
title: "Azure에서 Analysis Services 서버 aaaCreate | Microsoft Docs"
description: "Azure에서 toocreate Analysis Services 서버 인스턴스 하는 방법에 대해 알아봅니다."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 7f560216-8a9a-4d06-852e-48cf24deab19
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 3668f659039f79f3dd71498d1066e8682bf33228
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-analysis-services-server-in-azure-portal"></a>Azure Portal에서 Azure Analysis Services 서버 만들기
이 문서에서는 Azure 구독에서 Analysis Services 서버 리소스를 만드는 과정을 안내합니다.

## <a name="before-you-begin"></a>시작하기 전에
toocomplete 해야이 빠른 시작:

* **Azure 구독**: 방문 [Azure 무료 평가판](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate 계정.
* **Azure Active Directory**: 구독이 Azure Active Directory와 연결되어야 합니다. 고 toobe tooAzure Azure Active Directory의 계정으로 로그인 해야 합니다. Microsoft 계정은 지원되지 않습니다. toolearn 더 참조 [인증 및 사용자 권한을](analysis-services-manage-users.md)합니다.
* **리소스 그룹**: 기존 리소스 그룹을 사용하거나 [새 리소스 그룹을 만듭니다](../azure-resource-manager/resource-group-overview.md).

> [!NOTE]
> 서버를 만들면 새로운 유료 서비스가 생성될 수 있습니다. toolearn 더 참조 [Analysis Services 가격](https://azure.microsoft.com/pricing/details/analysis-services/)합니다.
> 
> 

## <a name="toocreate-a-server-in-azure-portal"></a>Azure 포털에서 서버 toocreate
1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.  
2. **+새로 만들기** > **데이터 + 분석** > **Analysis Services**를 클릭합니다.
3. Hello에 **Analysis Services** 블레이드에서 필수 hello 필드를 입력 하 고 다음 키를 누릅니다 **만들기**합니다.
   
    ![서버 만들기](./media/analysis-services-create-server/aas-create-server-blade.png)
   
   * **서버 이름**: 사용 된 고유 이름을 tooreference hello 서버를 입력 합니다.
   * **구독**:이 서버에 청구 hello 구독을 선택 합니다.
   * **리소스 그룹**: 이러한 컨테이너는 디자인 된 toohelp Azure 리소스 컬렉션을 관리 합니다. toolearn 더 참조 [리소스 그룹](../azure-resource-manager/resource-group-overview.md)합니다.
   * **위치**:이 Azure 데이터 센터 위치 호스트 서버 hello 합니다. 가장 큰 사용자 기반에 가장 가까운 위치를 선택합니다.
   * **가격 책정 계층**: 가격 책정 계층을 선택합니다. Too400 GB 테이블 형식 모델 지원 됩니다. toolearn 더 참조 [Azure Analysis Services 가격](https://azure.microsoft.com/pricing/details/analysis-services/)합니다.
4. **만들기**를 클릭합니다.

만드는 데 1분 이내, 대개 몇 초가 걸립니다. 선택한 경우 **tooPortal 추가**, tooyour 포털 toosee 새 서버로 이동 합니다. 너무 이동 또는**더 많은 서비스** > **Analysis Services** toosee 서버를 준비 합니다.

 ![대시보드](./media/analysis-services-create-server/aas-create-server-dashboard.png)


## <a name="next-steps"></a>다음 단계
서버를 만든 후 [모델 배포](analysis-services-deploy.md) tooit SSMS 또는 SSDT를 사용 하 여 합니다.

Tooinstall 필요한 tooyour 서버를 배포 하는 모델 tooon 온-프레미스 데이터 원본에 연결 된 경우는 [온-프레미스 데이터 게이트웨이](analysis-services-gateway.md) 네트워크의 컴퓨터에 있습니다.

