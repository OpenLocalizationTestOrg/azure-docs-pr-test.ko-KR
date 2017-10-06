---
title: "클라우드 서비스 (클래식 포털) aaaHow tooconfigure | Microsoft Docs"
description: "Azure에서 tooconfigure 클라우드 서비스 하는 방법에 대해 알아봅니다. Tooupdate hello 클라우드 서비스 구성 알아보고 원격 액세스 toorole 인스턴스를 구성 합니다."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 4902f79d-ea91-41ca-89a4-7c818180ee5f
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 1ea2320f97f667153f7984e4d61d373a6344cf6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-cloud-services"></a>TooConfigure 클라우드 서비스 하는 방법
> [!div class="op_single_selector"]
> * [Azure 포털](cloud-services-how-to-configure-portal.md)
> * [Azure 클래식 포털](cloud-services-how-to-configure.md)
> 
> 

Hello Azure 클래식 포털에서에서 클라우드 서비스에 대 한 가장 일반적으로 사용 하는 hello 설정을 구성할 수 있습니다. 또는 구성 파일을 직접 서비스 구성 파일 tooupdate 다운로드 하 고 hello 구성 변경 내용으로 업데이트 하는 hello 파일 및 업데이트 hello 클라우드 서비스 업로드 tooupdate 사용 하려는 경우. 두 가지 경우 모두 hello 구성 업데이트 tooall 역할 인스턴스에 게시 됩니다.

hello Azure 클래식 포털에서는 있습니다 너무[Azure 클라우드 서비스에서 역할에 대 한 원격 데스크톱 연결을 사용 하도록 설정](cloud-services-role-enable-remote-desktop.md)

Azure 수만 99.95% 서비스 가용성을 보장 하는 동안 hello 구성 업데이트 모든 역할에 대 한 두 개 이상의 역할 인스턴스가 있는 경우. 수 있도록 하나 가상 컴퓨터 tooprocess 클라이언트 요청 다른 hello를 업데이트 하는 동안 합니다. 자세한 내용은 [서비스 수준 계약](https://azure.microsoft.com/support/legal/sla/)을 참조하세요.

## <a name="change-a-cloud-service"></a>클라우드 서비스 변경하기
1. Hello에 [Azure 클래식 포털](http://manage.windowsazure.com/), 클릭 **클라우드 서비스**hello 클라우드 서비스의 hello 이름을 클릭 하 고 클릭 **구성**합니다.
   
    ![구성 페이지](./media/cloud-services-how-to-configure/CloudServices_ConfigurePage1.png)
   
    Hello에 **구성** 페이지, 구성 모니터링, 업데이트 역할 설정 하 고 있습니다 hello 게스트 운영 체제 및 역할 인스턴스에 대 한 패밀리를 선택 합니다. 
2. **모니터링**, 수준 tooVerbose 모니터링 집합 hello 또는 최소 하 고 자세한 정보 표시 모니터링에 필요한 hello 진단 연결 문자열을 구성 합니다.
3. 서비스 역할 (역할 그룹화 됨)에 대 한 설정에 따라 hello를 업데이트할 수 있습니다.
   
    * **설정** hello에 지정 된 기타 구성 설정의 hello 값을 수정 *ConfigurationSettings* hello 서비스 구성 (.cscfg) 파일의 요소입니다.

    * **인증서**  
        역할에 대 한 SSL 암호화에 사용 중인 hello 인증서 지문을 변경 합니다. 인증서 toochange 먼저 업로드 해야 hello 새 인증서 (hello에 **인증서** 페이지). Hello 역할 설정에 표시 되는 hello 인증서 문자열에서 hello 지문을 업데이트 합니다.
4. **운영 체제**, hello 운영 체제 제품군 또는 역할 인스턴스에 대 한 버전을 변경 하거나 선택할 수 있습니다 **자동** tooenable hello 현재 운영 체제 버전의 자동 업데이트 합니다. hello 운영 체제 설정 tooweb 역할 및 작업자 역할을 적용 하지만 가상 컴퓨터에는 영향을 주지 않습니다.
   
    배포 하는 동안 모든 역할 인스턴스에 hello 최신 운영 체제 버전은 설치 하 고 hello 운영 체제 기본적으로 자동으로 업데이트 됩니다. 
   
    필요한 경우 다른 운영 체제 버전에서 클라우드 서비스 toorun 프로그램에 대 한 호환성 요구 사항 때문에 코드에서 운영 체제 제품군 및 버전을 선택할 수 있습니다. 특정 운영 체제 버전을 선택 하면 hello 클라우드 서비스에 대 한 자동 운영 체제 업데이트가 일시 중지 됩니다. Tooensure 해야 hello 운영 체제 업데이트를 수신 합니다.
   
    앱 hello 최신 운영 체제 버전에 포함 된 모든 호환성 문제를 해결 하는 경우 사용할 수 있습니다 자동 운영 체제 업데이트 hello 운영 체제 버전을 설정 하 여 너무**자동**합니다. 
   
    ![OS 설정](./media/cloud-services-how-to-configure/CloudServices_ConfigurePage_OSSettings.png)
5. toosave 구성 설정을 toohello 역할 인스턴스 푸시를 클릭 하 고 **저장**합니다. (클릭 **취소** toocancel hello 변경 합니다.) **저장** 및 **취소** 설정을 변경한 후 toohello 명령 모음에 추가 됩니다.

## <a name="update-a-cloud-service-configuration-file"></a>클라우드 서비스 구성 파일 업데이트
1. Hello 현재 구성 사용 하 여 클라우드 서비스 구성 파일 (.cscfg)을 다운로드 합니다. Hello에 **구성** hello 클라우드 서비스에 대 한 페이지 **다운로드**합니다. 클릭 **저장**, 하거나 클릭 **다른 이름으로 저장** toosave hello 파일입니다.
2. Hello 서비스 구성 파일을 업데이트 한 후 업로드 하 고 hello 구성 업데이트를 적용 합니다.
   
   1. Hello에 **구성** 페이지 **업로드**합니다.
      
       ![구성 업로드](./media/cloud-services-how-to-configure/CloudServices_UploadConfigFile.png)
   2. **구성 파일**를 사용 하 여 **찾아보기** tooselect hello.cscfg 파일을 업데이트 합니다.
   3. 클라우드 서비스에 인스턴스가 하나만 있는 모든 역할이 있는 경우 선택 hello **하나 이상의 역할 단일 인스턴스가 포함 된 경우에 구성을 적용** 역할 tooproceed hello에 대 한 확인란 tooenable hello 구성 업데이트 합니다.
      
       모든 역할에 대해 두 개 이상의 인스턴스를 정의하지 않는 경우 Azure는 서비스 구성 업데이트 과정에서 최소 99.95%의 클라우드 서비스 가용성을 보장할 수 없습니다. 자세한 내용은 [서비스 수준 계약](https://azure.microsoft.com/support/legal/sla/)을 참조하세요.
   4. **확인** (확인 표시)을 클릭합니다. 

## <a name="next-steps"></a>다음 단계
* 너무 방법에 대해 알아봅니다[클라우드 서비스 배포](cloud-services-how-to-create-deploy.md)합니다.
* [사용자 지정 도메인 이름](cloud-services-custom-domain-name.md)구성
* [클라우드 서비스를 관리합니다](cloud-services-how-to-manage.md).
* [Azure 클라우드 서비스의 역할에 대해 원격 데스크톱 연결 사용](cloud-services-role-enable-remote-desktop.md)
* [SSL 인증서](cloud-services-configure-ssl-certificate.md)구성

