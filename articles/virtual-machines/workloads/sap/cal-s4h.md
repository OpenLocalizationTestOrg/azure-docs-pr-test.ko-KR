---
title: "SAP S/4HANA 또는 Azure VM에서 BW/4HANA aaaDeploy | Microsoft Docs"
description: "Azure VM에서 SAP S/4HANA 또는 BW/4HANA 배포"
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 44bbd2b6-a376-4b5c-b824-e76917117fa9
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 09/15/2016
ms.author: hermannd
ms.openlocfilehash: 7e57f7daa7667b7c7dbcb86f6892a54e4295b74c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-sap-s4hana-or-bw4hana-on-azure"></a>Azure에서 SAP S/4HANA 또는 BW/4HANA 배포
이 문서를 사용 하 여 Azure에서 S/4HANA toodeploy SAP 클라우드 어플라이언스에 라이브러리 (SAP CAL) 3.0 hello 하는 방법을 설명 합니다. toodeploy hello를 수행 하는 다른 SAP HANA 기반 솔루션 BW/4HANA 같은 동일한 단계입니다.

> [!NOTE]
SAP CAL hello에 대 한 자세한 내용을 보려면 이동 toohello [SAP 클라우드 어플라이언스에 라이브러리](https://cal.sap.com/) 웹 사이트입니다. SAP 역시 hello에 대 한 블로그 [SAP 클라우드 어플라이언스에 라이브러리 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience)합니다.

> [!NOTE]
2017 년 5 월 29의 hello Azure 리소스 관리자 배포 모델을 사용할 수 있는 클래식 배포 toohello 보다 toodeploy hello SAP CAL 모델 또한 합니다. Hello 새 리소스 관리자 배포 모델을 사용 하 고 hello 클래식 배포 모델을 무시 하는 것이 좋습니다.

## <a name="step-by-step-process-toodeploy-hello-solution"></a>단계별 프로세스 toodeploy hello 솔루션

스크린 샷의 순서 따르면 hello를 사용 하 여 Azure에서 S/4HANA toodeploy SAP CAL hello 하는 방법을 보여 줍니다. hello 프로세스가 작동 하는 hello BW/4HANA 같은 다른 솔루션에 동일 합니다.

hello **솔루션** 페이지 중 일부가 나와 hello CAL SAP HANA 기반 솔루션을 사용할 수 있는 Azure에서. **SAP S/4HANA 1610 FPS01, Fully-Activated 기기** hello 중간 행에:

![SAP CAL 솔루션](./media/cal-s4h/s4h-pic-1c.png)

### <a name="create-an-account-in-hello-sap-cal"></a>SAP CAL hello에 계정 만들기
1. toosign hello에 대 한 SAP CAL toohello에 처음으로 SAP S-사용자 또는 다른 사용자가 sap 등록을 사용 합니다. Azure의 hello SAP CAL toodeploy 기기에서 사용 되는 SAP CAL 계정을 정의 합니다. Hello 계정 정의 해야 합니다.

    a. (리소스 관리자 또는 클래식) Azure의 hello 배포 모델을 선택 합니다.

    b. Azure 구독을 입력합니다. SAP CAL 계정 tooone 구독에만 할당할 수 있습니다. 둘 이상의 구독이 필요한 경우 다른 SAP CAL 계정이 toocreate 필요 합니다.

    c. Azure 구독에 hello SAP CAL 권한 toodeploy를 제공 합니다.

    > [!NOTE]
    hello 다음 단계에서 SAP CAL toocreate 리소스 관리자 배포를 고려 하는 방법을 보여 줍니다. 연결 된 toohello 클래식 배포 모델에 해당 하는 SAP CAL 계정을 이미 있는 경우 있습니다 *필요* toofollow 이러한 단계 toocreate 새 SAP CAL 계정. 새 SAP CAL 계정 hello toodeploy hello 리소스 관리자 모델에 필요합니다.

2. 새 SAP CAL 계정을 만듭니다. hello **계정** 페이지 Azure에 대 한 세 가지 선택 항목을 표시 합니다. 

    a. **Microsoft Azure (클래식)** hello 클래식 배포 모델 이며 더 이상 기본 설정입니다.

    b. **Microsoft Azure** 는 hello 새 리소스 관리자 배포 모델입니다.

    c. **Windows Azure 21vianet이 운영** 중국 hello 클래식 배포 모델을 사용 하는 옵션입니다.

    hello 리소스 관리자 모델에서는 toodeploy 선택 **Microsoft Azure**합니다.

    ![SAP CAL 계정 세부 정보](./media/cal-s4h/s4h-pic-2a.png)

3. Azure hello 입력 **구독 ID** 있는 hello Azure 포털에서 확인할 수 있습니다.

   ![SAP CAL 계정](./media/cal-s4h/s4h-pic3c.png)

4. 정의한 hello Azure 구독에 tooauthorize hello SAP CAL toodeploy, 클릭 **Authorize**합니다. 다음 페이지 hello hello 브라우저 탭에 나타납니다.

   ![Internet Explorer 클라우드 서비스 로그인](./media/cal-s4h/s4h-pic4c.png)

5. 둘 이상의 사용자 목록에 hello Microsoft 계정으로 연결 된 toobe hello coadministrator의 hello 선택한 Azure 구독을 선택 합니다. 다음 페이지 hello hello 브라우저 탭에 나타납니다.

   ![Internet Explorer 클라우드 서비스 확인](./media/cal-s4h/s4h-pic5a.png)

6. **Accept**를 클릭합니다. Hello 권한 부여에 성공한 경우 다시 hello SAP CAL 계정 정의 표시 됩니다. 짧은 시간 후 메시지 hello 권한 부여 프로세스 성공적으로 수행 되었는지 확인 합니다.

7. tooassign hello 새로 만든 SAP CAL 계정 tooyour 사용자를 입력 하면 **사용자 ID** 에 텍스트 상자 오른쪽 hello에 hello 및 클릭 **추가**합니다.

   ![계정 toouser 연결](./media/cal-s4h/s4h-pic8a.png)

8. tooassociate toosign toohello SAP CAL에서에서 사용 하는 hello 사용자와 계정을 클릭 **검토**합니다. 
 
9. 사용자 및 새로 만든 hello SAP CAL 계정 간의 toocreate hello 연결 클릭 **만들기**합니다.

   ![사용자 tooSAP CAL 계정 연결](./media/cal-s4h/s4h-pic9b.png)

다음을 할 수 있는 SAP CAL 계정을 성공적으로 만들었습니다.

- Hello 리소스 관리자 배포 모델을 사용 합니다.
- Azure 구독에 SAP 시스템을 배포합니다.

이제 Azure에서 사용자 구독에 S/4HANA toodeploy를 시작할 수 있습니다.

> [!NOTE]
계속하기 전에 Azure H 시리즈 VM에 대한 Azure 코어 할당량이 확인합니다. Hello 순간에 SAP CAL hello 사용 하 여 H 시리즈 Vm의 Azure toodeploy hello SAP HANA 기반 솔루션의 일부입니다. Azure 구독은 H 시리즈에 대한 H 시리즈 코어 할당량이 없을 수 있습니다. 이 경우 toocontact Azure 지원 tooget 16 H 시리즈 코어 할당량을 할 수 있습니다.

> [!NOTE]
Azure에서 SAP CAL hello에서 솔루션을 배포할 때 Azure 지역 하나만 선택할 수 있는 경우가 있습니다. SAP CAL hello에서 제안한 하나는 hello 이외의 Azure 지역에 toodeploy toopurchase SAP에서 CAL 구독 사용 해야 합니다. 또한 해야 tooopen SAP toohave 포함 된 메시지를 CAL 계정 설정 toodeliver hello 처음 제안 된 것 이외의 Azure 지역에 합니다.

### <a name="deploy-a-solution"></a>솔루션 배포

보겠습니다 hello에서 솔루션을 배포 **솔루션** hello SAP CAL의 페이지입니다. SAP CAL hello에 두 개의 시퀀스 toodeploy가 있습니다.

- 배포 된 하나의 페이지 toodefine hello 시스템 toobe를 사용 하는 기본 순서
- VM 크기에 특정 선택 사항을 제공하는 고급 시퀀스 

여기에 기본 경로 toodeployment hello에 대해서도 설명 합니다.

1. Hello에 **계정 세부 정보** 페이지를 해야 합니다.

    a. SAP CAL 계정을 선택합니다. (연결된 toodeploy hello 리소스 관리자 배포 모델에 해당 하는 계정을 사용 합니다.)

    b. 인스턴스 **이름**을 입력합니다.

    c. Azure **지역**을 선택합니다. SAP CAL hello 영역을 제안합니다. 다른 Azure 지역에 필요한 SAP CAL 구독이 없는 경우에 SAP와 CAL tooorder 구독이 필요 합니다.

    d. 마스터 입력 **암호** 8 또는 9 개 문자의 hello 솔루션에 대 한 합니다. hello 암호 hello 관리자 hello 다른 구성 요소에 사용 됩니다.

   ![SAP CAL 기본 모드: 인스턴스 만들기](./media/cal-s4h/s4h-pic10a.png)

2. 클릭 **만들기**, hello 메시지 상자가 표시 되 면에서 클릭 하 고 **확인**합니다.

   ![SAP CAL 지원되는 VM 크기](./media/cal-s4h/s4h-pic10b.png)

3. Hello에 **개인 키** 대화 상자를 클릭 **저장소** toostore hello hello SAP CAL의에서 개인 키입니다. hello 개인 키에 대 한 암호 보호 toouse 클릭 **다운로드**합니다. 

   ![SAP CAL 개인 키](./media/cal-s4h/s4h-pic10c.png)

4. 읽기 hello SAP CAL **경고** 클릭 하 고 메시지, **확인**합니다.

   ![SAP CAL 경고](./media/cal-s4h/s4h-pic10d.png)

    이제 hello 배포 수행이 됩니다. 일정 시간이 지난 후 hello 솔루션 (hello SAP CAL 예상치를 제공)의 hello 크기와 복잡성에 따라 hello 상태가 표시 됩니다으로 활성 상태이 고 사용 하기 위해 준비 합니다.

5. toofind hello 가상 컴퓨터를 사용 하 여 수집한 한 리소스 그룹에 연결 된 다른 리소스 hello, Azure 포털 toohello 이동: 

   ![Hello 새 포털에 배포 된 SAP CAL 개체](./media/cal-s4h/sapcaldeplyment_portalview.png)

6. Hello SAP CAL 포털에서 hello 상태가으로 표시 **활성**합니다. tooconnect toohello 솔루션 클릭 **연결**합니다. 다양 한 옵션 tooconnect toohello 서로 다른 구성 요소는이 솔루션 내에서 배포 됩니다.

   ![SAP CAL 인스턴스](./media/cal-s4h/active_solution.png)

7. 클릭 하 여 hello 옵션 tooconnect 배포 toohello 시스템 중 하나를 사용 하려면 먼저 **시작 가이드**합니다. 

   ![Toohello 인스턴스 연결](./media/cal-s4h/connect_to_solution.png)

    hello 설명서 이름 각 hello 연결 방법에 대 한 사용자가 hello 합니다. 해당 사용자에 대 한 hello 암호 hello 배포 프로세스의 hello 맨 앞에서 정의한 toohello 마스터 암호를 설정 됩니다. Hello 설명서에서 기능적 다른 사용자가 사용할 수 있는 암호를 함께 나열 됩니다에 toohello toosign 시스템을 배포 합니다. 

    예를 들어 hello Windows 원격 데스크톱 컴퓨터에 SAP GUI가 사전 설치 되어 있는 hello를 사용 하는 경우 hello S/4 시스템 다음과 같이 표시 될 수 있습니다.

   ![Hello에 SM50 SAP GUI를 사전 설치](./media/cal-s4h/gui_sm50.png)

    또는 다음과 같은 hello 인스턴스 형식 hello DBACockpit을 사용 하는 경우:

   ![Hello DBACockpit SAP GUI에 SM50](./media/cal-s4h/dbacockpit.png)

몇 시간 이내에 정상 SAP S/4 어플라이언스가 Azure에 배포됩니다.

SAP CAL 구독을 구입한 경우, SAP Azure에서 SAP CAL hello 통해 배포를 완벽 하 게 지원 합니다. hello 지원 큐는 BC-VCM-CAL입니다.







