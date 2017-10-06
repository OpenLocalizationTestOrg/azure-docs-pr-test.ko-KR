---
title: "aaaHow toocreate 클라우드 서비스 및 배포 | Microsoft Docs"
description: "자세한 내용은 방법 toocreate hello Azure 포털을 사용 하 여 클라우드 서비스 및 배포 합니다."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 56ea2f14-34a2-4ed9-857c-82be4c9d0579
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: dc8b81a594f3514e662c49c9a46a33da8a551f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-deploy-a-cloud-service"></a>어떻게 toocreate 클라우드 서비스 및 배포
> [!div class="op_single_selector"]
> * [Azure 포털](cloud-services-how-to-create-deploy-portal.md)
> * [Azure 클래식 포털](cloud-services-how-to-create-deploy.md)
>
>

hello Azure 포털 toocreate 있습니다에 대 한 두 가지 방법을 제공 하 고 클라우드 서비스 배포: *빠른 생성* 및 *사용자 지정 만들기*합니다.

이 문서에서는 toouse 메서드 toocreate 빠른 생성 새 클라우드 서비스는 hello 하 고 다음 사용 하는 방법에 대해 설명 **업로드** tooupload 하 고 Azure에서 클라우드 서비스 패키지를 배포 합니다. 이 방법을 사용 하면 hello Azure 포털에서 작업을 진행 하면서 요구 사항을 모두 완료 하기 위한 편리 하 게 사용할 수 있는 링크를 설정 합니다. 을 사용 하는 클라우드 서비스를 만들 경우 준비 toodeploy hello에 둘 다를 수행할 수 있습니다 동시 사용자 지정 만들기 사용 합니다.

> [!NOTE]
> 클라우드 서비스에서 VSTS Visual Studio Team Services () toopublish 하려는 경우 빠른 생성을 사용 하 고 hello Azure 빠른 시작 또는 hello 대시보드에서 VSTS 게시를 설정 합니다. 자세한 내용은 참조 [Visual Studio Team Services를 사용 하 여 지속적인 업데이트 tooAzure][TFSTutorialForCloudService], 또는 hello에 대 한 도움말을 참조 하십시오 **빠른 시작** 페이지.
>
>

## <a name="concepts"></a>개념
세 가지 구성 요소가 필요한 toodeploy Azure에서 클라우드 서비스로 응용 프로그램:

* **서비스 정의**  
  hello 클라우드 서비스 정의 파일 (.csdef) hello 역할 수를 포함 하 여 hello 서비스 모델을 정의 합니다.
* **서비스 구성**  
  hello 클라우드 서비스 구성 파일 (.cscfg) hello 클라우드 서비스 및 hello 역할 인스턴스 수를 비롯 한 개별 역할에 대 한 구성 설정을 제공 합니다.
* **서비스 패키지**  
  hello 서비스 패키지 (.cspkg) hello 응용 프로그램 코드 및 구성과 hello 서비스 정의 파일을 포함합니다.

이 대 한 자세히 알아볼 수 있습니다 및 방법을 toocreate 패키지 [여기](cloud-services-model-and-package.md)합니다.

## <a name="prepare-your-app"></a>앱 준비
클라우드 서비스를 배포 하기 전에 응용 프로그램 코드와 클라우드 서비스 구성 파일 (.cscfg)에서 hello 클라우드 서비스 패키지 (.cspkg)를 만들어야 합니다. Azure SDK hello 이러한 필수 배포 파일을 준비 하기 위한 도구를 제공 합니다. Hello에서 hello SDK를 설치할 수 있습니다 [Azure 다운로드](https://azure.microsoft.com/downloads/) toodevelop 원하는 hello 언어로 응용 프로그램 코드 페이지입니다.

세 가지 클라우드 서비스 기능은 서비스 패키지를 내보내기 전에 특별히 구성해야 합니다.

* Toodeploy 데이터 암호화에 대 한 Secure Sockets Layer (SSL)를 사용 하는 클라우드 서비스를 원하는 경우 [응용 프로그램을 구성](cloud-services-configure-ssl-certificate-portal.md#modify) SSL에 대 한 합니다.
* Tooconfigure 원격 데스크톱 연결 toorole 인스턴스를 원하는 경우 [hello 역할 구성](cloud-services-role-enable-remote-desktop-new-portal.md) 원격 데스크톱에 대 한 합니다.
* Tooconfigure를 클라우드 서비스에 대 한 모니터링 세부 정보 표시 하려는 경우 hello 클라우드 서비스에 대 한 Azure 진단을 사용 합니다. *최소 모니터링* (hello 기본 수준 모니터링) 역할 인스턴스 (가상 컴퓨터)에 대 한 hello 호스트 운영 체제에서 수집한 성능 카운터를 사용 합니다. *자세한 정보 표시 모니터링* hello 역할 인스턴스 tooenable 보다 자세하게 분석 응용 프로그램 처리 하는 동안 발생 하는 문제 내에서 성능 데이터를 기반으로 하는 추가 메트릭을 수집 합니다. tooenable Azure 진단을 참조 하는 방법에 대해 toofind [Azure에서 진단 사용](cloud-services-dotnet-diagnostics.md)합니다.

해야 클라우드 서비스 웹 역할 또는 작업자 역할의 배포와 toocreate [hello 서비스 패키지 만들기](cloud-services-model-and-package.md#servicepackagecspkg)합니다.

## <a name="before-you-begin"></a>시작하기 전에
* Hello Azure SDK를 설치 하지 않은 경우 클릭 **Azure SDK 설치** tooopen hello [Azure 다운로드 페이지](https://azure.microsoft.com/downloads/), 한 후 hello를 원하는 언어 toodevelop 코드에 대 한 hello SDK를 다운로드 합니다. (해야 합니다. 영업 기회 toodo이 나중에.)
* 인증서를 요구 하는 모든 역할 인스턴스를 hello 인증서를 만듭니다. 클라우드 서비스에는 개인 키가 포함된 .pfx 파일이 필요합니다. Hello 클라우드 서비스 배포를 만들 때 hello 인증서 tooAzure를 업로드할 수 있습니다.

## <a name="create-and-deploy"></a>만들기 및 배포
1. Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.
2. 클릭 **새로 만들기 > 계산**, 한 다음 tooand 클릭 아래로 스크롤하여 **클라우드 서비스**합니다.

    ![클라우드 서비스 게시](media/cloud-services-how-to-create-deploy-portal/create-cloud-service.png)
3. 새 hello에 **클라우드 서비스** 블레이드에서 hello에 대 한 값을 입력 **DNS 이름**합니다.
4. 새 **리소스 그룹** 을 만들거나 기존 항목을 선택합니다.
5. **위치**를 선택합니다.
6. **패키지**를 클릭합니다. Hello 열립니다 **패키지 업로드** 블레이드입니다. Hello 필수 필드를 입력 합니다. 역할에 단일 인스턴스가 포함된 경우 **단일 인스턴스가 포함된 역할이 하나 이상 있는 경우에도 배포합니다.** 가 선택되어 있어야 합니다.
7. **배포 시작** 이 선택되어 있는지 확인합니다.
8. 클릭 **확인** hello 닫힙니다 **패키지 업로드** 블레이드입니다.
9. 모든 인증서 tooadd가 클릭 **만들기**합니다.

    ![클라우드 서비스 게시](media/cloud-services-how-to-create-deploy-portal/select-package.png)

## <a name="upload-a-certificate"></a>인증서 업로드
배포 패키지 되었으면 [toouse 인증서 구성](cloud-services-configure-ssl-certificate-portal.md#modify), 이제 hello 인증서를 업로드할 수 있습니다.

1. 선택 **인증서**, 등과 hello **인증서 추가** 블레이드에서 hello SSL 인증서.pfx 파일을 선택 하 고 hello를 입력 하십시오 **암호** hello 인증서에 대 한
2. 클릭 **연결 인증서**, 클릭 하 고 **확인** hello에 **인증서 추가** 블레이드입니다.
3. 클릭 **만들기** hello에 **클라우드 서비스** 블레이드입니다. Hello 배포 hello에 도달한 경우 **준비** 상태, toohello 다음 단계를 진행할 수 있습니다.

    ![클라우드 서비스 게시](media/cloud-services-how-to-create-deploy-portal/attach-cert.png)

## <a name="verify-your-deployment-completed-successfully"></a>배포가 완료되었는지 확인
1. Hello 클라우드 서비스 인스턴스를 클릭 합니다.

    hello 상태가 표시 hello 서비스가 임을 **실행**합니다.
2. 아래 **Essentials**, hello 클릭 **사이트 URL** tooopen 웹 브라우저에서 클라우드 서비스입니다.

    ![CloudServices_QuickGlance](./media/cloud-services-how-to-create-deploy-portal/running.png)

[TFSTutorialForCloudService]: http://go.microsoft.com/fwlink/?LinkID=251796

## <a name="next-steps"></a>다음 단계
* [클라우드 서비스의 일반 구성](cloud-services-how-to-configure-portal.md)
* [사용자 지정 도메인 이름](cloud-services-custom-domain-name-portal.md)구성
* [클라우드 서비스를 관리합니다](cloud-services-how-to-manage-portal.md).
* [SSL 인증서](cloud-services-configure-ssl-certificate-portal.md)구성
