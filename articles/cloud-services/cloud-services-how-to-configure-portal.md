---
title: "클라우드 서비스 (포털) aaaHow tooconfigure | Microsoft Docs"
description: "Azure에서 tooconfigure 클라우드 서비스 하는 방법에 대해 알아봅니다. Tooupdate hello 클라우드 서비스 구성 알아보고 원격 액세스 toorole 인스턴스를 구성 합니다. 이러한 예제는 hello Azure 포털을 사용합니다."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 7308f3c0-825e-499d-bfa5-c60f86371921
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/07/2016
ms.author: adegeo
ms.openlocfilehash: 969a08558473e8c79153192942bfda587eb5ada5
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

Hello Azure 포털에서에서 클라우드 서비스에 대 한 가장 일반적으로 사용 하는 hello 설정을 구성할 수 있습니다. 또는 구성 파일을 직접 서비스 구성 파일 tooupdate 다운로드 하 고 hello 구성 변경 내용으로 업데이트 하는 hello 파일 및 업데이트 hello 클라우드 서비스 업로드 tooupdate 사용 하려는 경우. 두 가지 경우 모두 hello 구성 업데이트 tooall 역할 인스턴스에 게시 됩니다.

에 클라우드 서비스 역할 또는 원격 데스크톱의 hello 인스턴스를 관리할 수 있습니다.

Azure 수만 99.95% 서비스 가용성을 보장 하는 동안 hello 구성 업데이트 모든 역할에 대 한 두 개 이상의 역할 인스턴스가 있는 경우. 수 있도록 하나 가상 컴퓨터 tooprocess 클라이언트 요청 다른 hello를 업데이트 하는 동안 합니다. 자세한 내용은 [서비스 수준 계약](https://azure.microsoft.com/support/legal/sla/)을 참조하세요.

## <a name="change-a-cloud-service"></a>클라우드 서비스 변경하기
Opening hello 후 [Azure 포털](https://portal.azure.com/), tooyour 클라우드 서비스를 이동 합니다. 여기에서 여러 항목을 관리할 수 있습니다.

![설정 페이지](./media/cloud-services-how-to-configure-portal/cloud-service.png)

hello **설정** 또는 **모든 설정을** 링크 hello 개방 되므로 **설정** hello를 변경할 수 있는 블레이드 **속성**, hello 변경 **구성**, hello 관리 **인증서**, 설치 **규칙 경고**, 고 hello 관리 **사용자** 대 한 액세스 권한이 toothis 클라우드 서비스입니다.

![Azure 클라우드 서비스 설정 블레이드](./media/cloud-services-how-to-configure-portal/cs-settings-blade.png)

### <a name="manage-guest-os-version"></a>게스트 OS 버전 관리

기본적으로 Azure Windows Server 2016 같은 게스트 OS toohello 최신 지원 되는 이미지, 서비스 구성 (.cscfg)에 지정 된 OS 제품군 hello 내에서 주기적으로 업데이트 합니다.

특정 운영 체제 버전 tootarget 해야 할 경우 hello에 설정할 수 있습니다 **구성** 블레이드입니다.

![OS 버전 설정](./media/cloud-services-how-to-configure-portal/cs-settings-config-guestosversion.png)


>[!IMPORTANT]
> 특정 OS 버전을 선택하면 자동 OS 업데이트가 사용되지 않도록 설정되며 패치는 사용자가 책임지고 진행해야 합니다. 업데이트를 수신 하는 역할 인스턴스 또는 응용 프로그램 toosecurity 취약점이 노출 될 수 있습니다를 확인 해야 합니다.

## <a name="monitoring"></a>모니터링
경고 tooyour 클라우드 서비스를 추가할 수 있습니다. **설정** > **경고 규칙** > **경고 추가**를 클릭합니다.

![](./media/cloud-services-how-to-configure-portal/cs-alerts.png)

여기에서 경고를 설정할 수 있습니다. Hello로 **메트릭을** 드롭다운 상자, 데이터 형식에 따라 hello에 대 한 경고를 설정할 수 있습니다.

* 디스크 읽기
* 디스크 쓰기
* 네트워크 입력
* 네트워크 출력
* CPU 비율

![](./media/cloud-services-how-to-configure-portal/cs-alert-item.png)

### <a name="configure-monitoring-from-a-metric-tile"></a>메트릭 타일에서 모니터링 구성
사용 하는 대신 **설정** > **경고 규칙**, hello에 hello 메트릭 타일 중 하나를 클릭할 수 있는 **모니터링** hello 섹션 **클라우드 서비스** 블레이드입니다.

![클라우드 서비스 모니터링](./media/cloud-services-how-to-configure-portal/cs-monitoring.png)

여기에서 hello 타일을 함께 사용 하는 hello 차트를 사용자 지정 하거나 경고 규칙을 추가할 수 있습니다.

## <a name="reboot-reimage-or-remote-desktop"></a>다시 부팅, 이미지로 다시 설치 또는 원격 데스크톱
이 이번에 hello를 사용 하 여 원격 데스크톱을 구성할 수 없습니다 **Azure 포털**합니다. 그러나 설정할 수 있습니다 통해 hello [Azure 클래식 포털](cloud-services-role-enable-remote-desktop.md), [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md), 또는 [Visual Studio](../vs-azure-tools-remote-desktop-roles.md)합니다.

먼저, hello 클라우드 서비스 인스턴스에 대해을 클릭 합니다.

![클라우드 서비스 인스턴스](./media/cloud-services-how-to-configure-portal/cs-instance.png)

하면 블레이드 hello에서 원격 데스크톱 연결을 시작, hello 인스턴스 또는 원격으로 이미지로 다시 설치 (새 이미지가 포함 된 시작) hello 인스턴스를 원격으로 다시 부팅 수 있습니다.

![클라우드 서비스 인스턴스 단추](./media/cloud-services-how-to-configure-portal/cs-instance-buttons.png)

## <a name="reconfigure-your-cscfg"></a>.cscfg 다시 구성
Tooreconfigure hello 통해 클라우드 서비스를 할 수 있습니다 [서비스 구성 (cscfg)](cloud-services-model-and-package.md#cscfg) 파일입니다. 먼저 toodownload 프로그램.cscfg 파일을 수정 하십시오. 다음 업로드 합니다.

1. Hello 클릭 **설정** 아이콘 또는 hello **모든 설정** hello tooopen 연결 **설정을** 블레이드 합니다.

    ![설정 페이지](./media/cloud-services-how-to-configure-portal/cloud-service.png)
2. Hello 클릭 **구성** 항목입니다.

    ![구성 블레이드](./media/cloud-services-how-to-configure-portal/cs-settings-config.png)
3. Hello 클릭 **다운로드** 단추입니다.

    ![다운로드](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-download.png)
4. Hello 서비스 구성 파일을 업데이트 한 후 업로드 하 고 hello 구성 업데이트를 적용 합니다.

    ![업로드](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-upload.png)
5. Hello.cscfg 파일을 선택 하 고 클릭 **확인**합니다.

## <a name="next-steps"></a>다음 단계
* 너무 방법에 대해 알아봅니다[클라우드 서비스 배포](cloud-services-how-to-create-deploy-portal.md)합니다.
* [사용자 지정 도메인 이름](cloud-services-custom-domain-name-portal.md)구성
* [클라우드 서비스를 관리합니다](cloud-services-how-to-manage-portal.md).
* [SSL 인증서](cloud-services-configure-ssl-certificate-portal.md)구성
