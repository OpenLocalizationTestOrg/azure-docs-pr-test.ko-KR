---
title: "aaaDeploy Azure에서 SAP ERP 6.0에 대 한 IDE EHP7 SP3 SAP | Microsoft Docs"
description: "Azure에서 SAP IDES EHP7 SP3 for SAP ERP 6.0 배포"
services: virtual-machines-windows
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 626c1523-1026-478f-bd8a-22c83b869231
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 09/16/2016
ms.author: hermannd
ms.openlocfilehash: 26d88c7b48a91d35602464c4f89ca7a30502c4b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-sap-ides-ehp7-sp3-for-sap-erp-60-on-azure"></a>Azure에서 SAP IDES EHP7 SP3 for SAP ERP 6.0 배포
이 문서에서는 설명 방법을 toodeploy는 SAP IDE 시스템 hello SAP 클라우드 어플라이언스에 라이브러리 (SAP CAL) 3.0 통해 Azure에서 SQL Server와 Windows 운영 체제 hello 실행 합니다. hello 스크린 샷을 hello 단계별 프로세스를 보여 줍니다. toodeploy를 다른 솔루션에 따라 동일한 단계를 hello 합니다.

SAP CAL, 이동 toohello hello로 toostart [SAP 클라우드 어플라이언스에 라이브러리](https://cal.sap.com/) 웹 사이트입니다. SAP에 hello에 대 한 블로그 새 [SAP 클라우드 어플라이언스에 라이브러리 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience)합니다. 

> [!NOTE]
2017 년 5 월 29의 hello Azure 리소스 관리자 배포 모델을 사용할 수 있는 클래식 배포 toohello 보다 toodeploy hello SAP CAL 모델 또한 합니다. Hello 새 리소스 관리자 배포 모델을 사용 하 고 hello 클래식 배포 모델을 무시 하는 것이 좋습니다.

Hello 일반 모델을 사용 하는 SAP CAL 계정을 이미 만든 경우 *다른 SAP CAL 계정 toocreate 필요한*합니다. 이 계정에 있어야 tooexclusively hello 리소스 관리자 모델을 사용 하 여 Azure에 배포 합니다.

SAP CAL toohello 로그인 한 후 첫 번째 페이지 hello 일반적으로 안내 toohello **솔루션** 페이지. SAP CAL hello에 제공 하는 hello 솔루션은 계속 증가 tooscroll 원하는 toofind hello 솔루션 상당한 할 수도 있습니다. Azure에서 단독으로 사용할 수 있는 강조 표시 하는 hello SAP IDE Windows 기반 솔루션 hello 배포 프로세스를 보여 줍니다.

![SAP CAL 솔루션](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic1.jpg)

### <a name="create-an-account-in-hello-sap-cal"></a>SAP CAL hello에 계정 만들기
1. toosign hello에 대 한 SAP CAL toohello에 처음으로 SAP S-사용자 또는 다른 사용자가 sap 등록을 사용 합니다. Azure의 hello SAP CAL toodeploy 기기에서 사용 되는 SAP CAL 계정을 정의 합니다. Hello 계정 정의 해야 합니다.

    a. (리소스 관리자 또는 클래식) Azure의 hello 배포 모델을 선택 합니다.

    b. Azure 구독을 입력합니다. SAP CAL 계정 tooone 구독에만 할당할 수 있습니다. 둘 이상의 구독이 필요한 경우 다른 SAP CAL 계정이 toocreate 필요 합니다.
    
    c. Azure 구독에 hello SAP CAL 권한 toodeploy를 제공 합니다.

    > [!NOTE]
    hello 다음 단계에서 SAP CAL toocreate 리소스 관리자 배포를 고려 하는 방법을 보여 줍니다. 연결 된 toohello 클래식 배포 모델에 해당 하는 SAP CAL 계정을 이미 있는 경우 있습니다 *필요* toofollow 이러한 단계 toocreate 새 SAP CAL 계정. 새 SAP CAL 계정 hello toodeploy hello 리소스 관리자 모델에 필요합니다.

2. toocreate 새 SAP CAL 계정, hello **계정** 페이지 Azure에 대 한 두 가지 선택 항목을 표시 합니다. 

    a. **Microsoft Azure (클래식)** hello 클래식 배포 모델 이며 더 이상 기본 설정입니다.

    b. **Microsoft Azure** 는 hello 새 리소스 관리자 배포 모델입니다.

    ![SAP CAL 계정](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic-2a.PNG)

    hello 리소스 관리자 모델에서는 toodeploy 선택 **Microsoft Azure**합니다.

    ![SAP CAL 계정](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic3c.PNG)

3. Azure hello 입력 **구독 ID** 있는 hello Azure 포털에서 확인할 수 있습니다. 

    ![SAP CAL 구독 ID](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic3c.PNG)

4. 정의한 hello Azure 구독에 tooauthorize hello SAP CAL toodeploy, 클릭 **Authorize**합니다. 다음 페이지 hello hello 브라우저 탭에 나타납니다.

    ![Internet Explorer 클라우드 서비스 로그인](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic4c.PNG)

5. 둘 이상의 사용자 목록에 hello Microsoft 계정으로 연결 된 toobe hello coadministrator의 hello 선택한 Azure 구독을 선택 합니다. 다음 페이지 hello hello 브라우저 탭에 나타납니다.

    ![Internet Explorer 클라우드 서비스 확인](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic5a.PNG)

6. **Accept**를 클릭합니다. Hello 권한 부여에 성공한 경우 다시 hello SAP CAL 계정 정의 표시 됩니다. 짧은 시간 후 메시지 hello 권한 부여 프로세스 성공적으로 수행 되었는지 확인 합니다.

7. tooassign hello 새로 만든 SAP CAL 계정 tooyour 사용자를 입력 하면 **사용자 ID** 에 텍스트 상자 오른쪽 hello에 hello 및 클릭 **추가**합니다. 

    ![계정 toouser 연결](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic8a.PNG)

8. tooassociate toosign toohello SAP CAL에서에서 사용 하는 hello 사용자와 계정을 클릭 **검토**합니다. 

9. 사용자 및 새로 만든 hello SAP CAL 계정 간의 toocreate hello 연결 클릭 **만들기**합니다.

    ![사용자 tooaccount 연결](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic9b.PNG)

다음을 할 수 있는 SAP CAL 계정을 성공적으로 만들었습니다.

- Hello 리소스 관리자 배포 모델을 사용 합니다.
- Azure 구독에 SAP 시스템을 배포합니다.

> [!NOTE]
Windows 및 SQL Server를 기반으로 하는 hello SAP IDE 솔루션을 배포 하려면 먼저 toosign SAP CAL 구독 하도록 할 수 있습니다. 그렇지 않으면 hello 솔루션 수로 표시 **잠금** hello 개요 페이지에 있습니다.

### <a name="deploy-a-solution"></a>솔루션 배포
1. SAP CAL 계정을 설정한 후 선택 **Windows 및 SQL Server에서 SAP IDE 솔루션 hello** 솔루션입니다. 클릭 **인스턴스 만들기**, hello 사용 현황 및 용어 상태를 확인 합니다. 

2. Hello에 **기본 모드: 인스턴스 만들기** 페이지를 해야 합니다.

    a. 인스턴스 **이름**을 입력합니다.

    b. Azure **지역**을 선택합니다. 여러 Azure 지역에서 제공 되는 SAP CAL 구독 tooget을 할 수 있습니다.

    c.  Hello 마스터 입력 **암호** hello 솔루션에서는 표시 된 것 처럼:

    ![SAP CAL 기본 모드: 인스턴스 만들기](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic10a.png)

3. **만들기**를 클릭합니다. 일정 시간이 지난 후 hello 솔루션 (hello SAP CAL 예상치를 제공)의 hello 크기와 복잡성에 따라 hello 상태는 표시으로 활성 상태이 고 사용 하기 위해 준비: 

    ![SAP CAL 인스턴스](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic12a.png)

4. SAP CAL hello toofind hello 리소스 그룹 및 모든 해당 개체에서 생성 된 toohello Azure 포털을 이동 하십시오. 동일한 인스턴스 이름을 SAP CAL hello에 제공 된 hello로 시작 hello 가상 컴퓨터를 찾을 수 있습니다.

    ![리소스 그룹 개체](./media/cal-ides-erp6-ehp7-sp3-sql/ides_resource_group.PNG)

5. Hello SAP CAL 포털에 배포 된 toohello 인스턴스 이동를 클릭 **연결**합니다. hello 다음 팝업 창에 표시 됩니다. 

    ![Toohello 인스턴스 연결](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic14a.PNG)

6. 클릭 하 여 hello 옵션 tooconnect 배포 toohello 시스템 중 하나를 사용 하려면 먼저 **시작 가이드**합니다. hello 설명서 이름 각 hello 연결 방법에 대 한 사용자가 hello 합니다. 해당 사용자에 대 한 hello 암호 hello 배포 프로세스의 hello 맨 앞에서 정의한 toohello 마스터 암호를 설정 됩니다. Hello 설명서에서 기능적 다른 사용자가 사용할 수 있는 암호를 함께 나열 됩니다에 toohello toosign 시스템을 배포 합니다.

    ![SAP 시작 설명서](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic15.jpg)

몇 시간 이내에 정상 SAP IDES 시스템이 Azure에 배포됩니다.

SAP CAL 구독을 구입한 경우, SAP Azure에서 SAP CAL hello 통해 배포를 완벽 하 게 지원 합니다. hello 지원 큐는 BC-VCM-CAL입니다.

