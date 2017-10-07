---
title: "Azure 클라우드 서비스에서 역할에 대 한 원격 데스크톱 연결 aaaEnable | Microsoft Docs"
description: "어떻게 tooconfigure azure 클라우드 서비스 응용 프로그램 tooallow 원격 데스크톱 연결"
services: cloud-services
documentationcenter: 
author: mmccrory
manager: timlt
editor: 
ms.assetid: 73ea1d64-1529-4d72-b58e-f6c10499e6bb
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: mmccrory
ms.openlocfilehash: 55d7043df571c2e88b04aa9ef01dc8ae1d6784f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a>Azure 클라우드 서비스의 역할에 대해 원격 데스크톱 연결 사용
> [!div class="op_single_selector"]
> * [Azure 포털](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [Azure 클래식 포털](cloud-services-role-enable-remote-desktop.md)
> * [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md)
> * [Visual Studio](../vs-azure-tools-remote-desktop-roles.md)
>
>

원격 데스크톱 사용 하면 Azure에서 실행 중인 역할의 tooaccess hello 데스크톱 있습니다. 원격 데스크톱 연결 tootroubleshoot를 사용할 수 있으며 실행 되는 동안 응용 프로그램 문제를 진단할 수 있습니다.

서비스 정의에 hello 원격 데스크톱 모듈을 포함 하 여 개발 하는 동안 원격 데스크톱 연결 사용자 역할에 사용할 수 또는 원격 데스크톱 확장 hello 통해 원격 데스크톱 tooenable를 선택할 수 있습니다. hello 선호 되는 방법은 toouse hello 원격 데스크톱 확장 hello tooredeploy 응용 프로그램 필요 없이 배포 된 후에 원격 데스크톱을 사용할 수 있습니다.

## <a name="configure-remote-desktop-from-hello-azure-portal"></a>Hello Azure 포털에서에서 원격 데스크톱을 구성 합니다.
Azure 포털 hello hello 원격 데스크톱 확장 방법을 사용 하 여 hello 응용 프로그램을 배포 후에 원격 데스크톱을 사용할 수 있도록 합니다. hello **원격 데스크톱** 클라우드 서비스에 대 한 블레이드 tooenable 원격 데스크톱을 사용 하면, tooconnect toohello 가상 컴퓨터를 사용 하는 변경 hello 로컬 관리자 계정, hello 인증서 인증에 사용 하 고 hello 설정 만료 날짜입니다.

1. 클릭 **클라우드 서비스**hello 클라우드 서비스의 hello 이름을 클릭 하 고 클릭 **원격 데스크톱**합니다.

    ![클라우드 서비스 원격 데스크톱](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop.png)

2. 선택한 모든 역할 또는 개별 역할에 대 한 원격 데스크톱 tooenable 원하는 여부 후 hello 전환기의 hello 값도 변경**Enabled**합니다.

3. 사용자 이름, 암호, 만료, 및 인증서에 대 한 hello 필수 필드를 입력 합니다.

    ![클라우드 서비스 원격 데스크톱](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Details.png)

   > [!WARNING]
   > 처음으로 원격 데스크톱을 사용하도록 설정한 후 확인(확인 표시)을 클릭하면 모든 역할 인스턴스가 다시 시작됩니다. 다시 부팅 hello 인증서 사용 되는 tooencrypt hello 암호 tooprevent hello 역할에 설치 되어야 합니다. tooprevent 다시 시작을 [hello 클라우드 서비스에 대 한 인증서 업로드](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) 다음 toothis 대화를 반환 합니다.
   >
   >
3. **역할**선택, 선택 하거나 tooupdate hello 역할 **모든** 모든 역할에 대 한 합니다.

4. 구성 업데이트를 마치면 **저장**을 클릭합니다. 사용자의 역할 인스턴스가 준비 tooreceive 연결 하기 전에 몇 분 정도 걸립니다.

## <a name="remote-into-role-instances"></a>원격으로 역할 인스턴스 액세스
Hello 역할에 원격 데스크톱 활성화 되 면 hello Azure 포털에서 직접 연결을 시작할 수 있습니다.

1. 클릭 **인스턴스** tooopen hello **인스턴스** 블레이드입니다.
2. 원격 데스크톱이 구성된 역할 인스턴스를 선택합니다.
3. 클릭 **연결** toodownload는 RDP hello 역할 인스턴스에 대 한 파일입니다.

    ![클라우드 서비스 원격 데스크톱](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Connect.png)

4. 클릭 **열려** 차례로 **연결** toostart hello 원격 데스크톱 연결 합니다.

>[!NOTE]
> 클라우드 서비스 NSG 뒤 대기 중임을 하는 경우에 포트에서 트래픽을 허용 하는 toocreate 규칙을 할 수 있습니다 **3389** 및 **20000**합니다.  원격 데스크톱은 포트 **3389**를 사용합니다.  클라우드 서비스 인스턴스 부하 분산이 되므로 어떤 인스턴스 tooconnect을 직접 제어할 수 없습니다.  hello *RemoteForwarder* 및 *RemoteAccess* 에이전트 RDP 트래픽을 관리 하 고 hello 클라이언트 toosend RDP 쿠키를 허용 및는 개별 인스턴스 tooconnect를 지정 합니다.  hello *RemoteForwarder* 및 *RemoteAccess* 에이전트에 해당 포트 필요 **20000*** 열 수 있는 NSG 있는 경우 차단 될 수 있습니다.

## <a name="additional-resources"></a>추가 리소스

[어떻게 tooConfigure 클라우드 서비스](cloud-services-how-to-configure.md)
[클라우드 서비스 FAQ-원격 데스크톱](cloud-services-faq.md)
