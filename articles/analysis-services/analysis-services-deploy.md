---
title: "SSDT를 사용 하 여 Analysis Services aaaDeploy tooAzure | Microsoft Docs"
description: "Azure Analysis Services 하는 테이블 형식 모델 tooan toodeploy 방법에 대해 알아봅니다 SSDT를 사용 하 여 서버입니다."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 5f1f0ae7-11de-4923-a3da-888b13a3638c
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/01/2017
ms.author: owend
ms.openlocfilehash: e3f3771fe32a37b9e0173c274080c647152edd4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-model-from-ssdt"></a>SSDT에서 모델 배포
Azure 구독에는 서버를 만들면 준비 toodeploy 테이블 형식 모델 데이터베이스 tooit 것입니다. SQL Server Data Tools (SSDT) toobuild를 사용할 수 있으며에서 작업 하는 테이블 형식 모델 프로젝트를 배포. 

## <a name="prerequisites"></a>필수 조건
시작 tooget를 해야 합니다.

* Azure의 **Analysis Services 서버** - toolearn 더 참조 [Azure Analysis Services 서버를 만들](analysis-services-create-server.md)합니다.
* **테이블 형식 모델 프로젝트** SSDT 또는 1200 hello 또는 더 높은 호환성 수준에서 기존 테이블 형식 모델에서. 만들어 본 적이 없나요? Hello 시도 [Adventure Works 인터넷 판매 테이블 형식 모델링 자습서](https://msdn.microsoft.com/library/hh231691.aspx)합니다.
* **온-프레미스 게이트웨이** -tooinstall 하나 이상의 데이터 원본을 온-프레미스 조직 네트워크의 경우 해야는 [온-프레미스 데이터 게이트웨이](analysis-services-gateway.md)합니다. hello 게이트웨이 hello 클라우드에서 서버 tooyour 온-프레미스 데이터 원본 tooprocess 및 새로 고침 데이터 hello 모델에서 연결을 위해 필요 합니다.

> [!TIP]
> 를 배포 하기 전에 테이블의 hello 데이터를 처리할 수 있는지 확인 합니다. SSDT에서 **모델** > **처리** > **모두 처리**를 클릭합니다. 처리가 실패하는 경우 성공적으로 배포할 수 없습니다.
> 
> 

## <a name="toodeploy-a-tabular-model-from-ssdt"></a>toodeploy SSDT에서 테이블 형식 모델

1. 를 배포 하기 전에 tooget hello 서버 이름이 필요 합니다. **Azure 포털** > 서버 > **개요** > **서버 이름**, hello 서버 이름 복사.
   
    ![Azure에서 서버 이름 가져오기](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. SSDT에서 > **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 hello 프로젝트 > **속성**합니다. 그런 다음 **배포** > **서버** hello 서버 이름을 붙여 넣습니다.   
   
    ![배포 서버 속성에 서버 이름을 붙여 넣습니다](./media/analysis-services-deploy/aas-deploy-deployment-server-property.png)
3. **솔루션 탐색기**에서 **속성**을 마우스 오른쪽 단추로 클릭한 후 **배포**를 클릭합니다. TooAzure에서 증명된 toosign 수도 있습니다.
   
    ![Tooserver 배포](./media/analysis-services-deploy/aas-deploy-deploy.png)
   
    배포 상태는 배포 및 두 hello 출력 창에 표시 됩니다.
   
    ![배포 상태](./media/analysis-services-deploy/aas-deploy-status.png)

그 tooit 있습니다!


## <a name="troubleshooting"></a>문제 해결
메타 데이터를 배포할 때 배포에 실패 될 SSDT tooyour 서버를 연결할 수 없습니다. SSMS를 사용 하 여 tooyour 서버를 연결할 수 있는지 확인 합니다. Hello hello 프로젝트에 대 한 배포 서버 속성이 올바른지 확인 합니다.

배포에 실패 한 테이블에 되므로 가능성이 서버 tooa 데이터 원본에 연결할 수 없습니다. 데이터 원본이 온-프레미스 조직 네트워크의 경우 수 있는지 tooinstall는 [온-프레미스 데이터 게이트웨이](analysis-services-gateway.md)합니다.

## <a name="next-steps"></a>다음 단계
테이블 형식 모델 배포 tooyour 서버를가지고 준비 tooconnect tooit 것입니다. 있습니다 수 [tooit SSMS를 사용 하 여 연결](analysis-services-manage.md) toomanage 것입니다. 할 수 있습니다 및 [tooit 클라이언트 도구를 사용 하 여 연결](analysis-services-connect.md) 같은 Power BI, Power BI Desktop 또는 Excel 및 보고서를 만들기 시작 합니다.

