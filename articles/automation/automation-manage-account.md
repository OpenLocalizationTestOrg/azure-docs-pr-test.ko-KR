---
title: "Azure 자동화 계정 aaaManage | Microsoft Docs"
description: "이 문서에서는 toomanage 인증서 갱신, 삭제 및 잘못 된 구성이 같은 자동화 계정 구성을 hello 하는 방법을 설명 합니다."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/13/2017
ms.author: magoedte
ms.openlocfilehash: 75e41f601a138d4e8853aa79dcbab6696a5e9fb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-automation-account"></a>Azure Automation 계정 관리
어느 시점 자동화 계정 만료 되기 전에 인증서가 필요 toorenew hello 합니다. 실행 계정이 해당 hello가 손상 된 경우 삭제 한 다시 만들 수 있습니다. 이 섹션에서는 어떻게 tooperform 이러한 작업 합니다.

## <a name="self-signed-certificate-renewal"></a>자체 서명된 인증서 갱신
hello 실행 계정에 대해 만든 자체 서명 된 인증서를 hello hello 생성 날짜 로부터 1 년에 만료 됩니다. 만료되기 전에 언제든지 갱신할 수 있습니다. Hello 현재 유효한 인증서를 갱신 하기 경우 보존된 tooensure 하는 최대 또는 적극적으로 실행 되 고 실행 계정 hello로 인증 하는 모든 runbook 부정적인 영향을 받지 않습니다. hello 인증서 만료 날짜까지 유효합니다.

> [!NOTE]
> 프로그램 엔터프라이즈 인증 기관에서 발급 한 인증서의 자동화 계정으로 실행 계정 toouse 구성한 경우이 옵션을 사용 하는 경우에 hello 엔터프라이즈 인증서 자체 서명 된 인증서로 바뀝니다.

toorenew hello 인증서, 다음 hello지 않습니다.

1. Hello Azure 포털에서에서 자동화 계정을 hello를 엽니다.

2. Hello에 **자동화 계정** hello에 블레이드 **속성 계정** 창 아래에서 **계정 설정**선택, **실행 계정**합니다.

    ![Automation 계정 속성 창](media/automation-manage-account/automation-account-properties-pane.png)
3. Hello에 **실행 계정** 속성 블레이드를 선택 하거나 hello 계정 또는 계정으로 실행 hello 클래식 계정으로 실행에 대 한 toorenew hello 인증서 원하는 합니다.

4. Hello에 **속성** 블레이드 hello에 대 한 계정 선택, 클릭 **갱신 인증서**합니다.

    ![실행 계정용 인증서 갱신](media/automation-manage-account/automation-account-renew-runas-certificate.png)

5. Hello 인증서를 갱신 하는 동안에 아래 hello 진행률을 추적할 수 **알림** hello 메뉴에서 합니다.

## <a name="delete-a-run-as-or-classic-run-as-account"></a>실행 또는 클래식 실행 계정 삭제
이 섹션에서는 설명 방법을 toodelete 다시 실행 또는 클래식 실행 계정을 만듭니다. 이 작업을 수행 하는 경우 자동화 계정을 hello 유지 됩니다. 다음 계정으로 실행 또는 클래식 계정으로 실행 계정을 삭제 한 후 hello Azure 포털에에서 다시 만들 수 있습니다.

1. Hello Azure 포털에서에서 자동화 계정을 hello를 엽니다.

2. Hello에 **자동화 계정** hello 계정 속성 창에서 선택 블레이드 **실행 계정**합니다.

3. Hello에 **실행 계정** toodelete 원하는 계정 속성 블레이드를 선택 하거나 hello 실행 계정 또는 클래식 계정으로 실행 합니다. 그런 다음 hello **속성** 블레이드 hello에 대 한 계정 선택, 클릭 **삭제**합니다.

 ![실행 계정 삭제](media/automation-manage-account/automation-account-delete-runas.png)

4. Hello 계정을 삭제 하는 동안에 아래 hello 진행률을 추적할 수 **알림** hello 메뉴에서 합니다.

5. Hello 계정을 삭제 한 후 다시 만들 수 있습니다이 hello에 **실행 계정** hello를 선택 하 여 속성 블레이드 생성 옵션 **Azure 실행 계정**합니다.

 ![Hello 자동화 계정으로 실행 계정을 다시 만드는](media/automation-manage-account/automation-account-create-runas.png)

## <a name="misconfiguration"></a>잘못된 구성
Hello 계정으로 실행 또는 클래식 실행 계정 toofunction에 필요한 일부 구성 항목 제대로 수 삭제 되거나 부적절 하 게 초기 설치 중에 생성 합니다. hello 항목은 다음과 같습니다.

* 인증서 자산
* 연결 자산
* 실행 계정은 hello 참가자 역할에서 제거 되었습니다.
* Azure AD의 서비스 주체 또는 응용 프로그램

위의 hello 및 잘못 된 구성의 다른 인스턴스 hello 자동화 계정을 검색 hello 변경의 상태를 표시 하 고 *완료 안 됨* hello에 **실행 계정** hello에 대 한 속성 블레이드 계정입니다.

![불완전 실행 계정 구성 상태](media/automation-manage-account/automation-account-runas-incomplete-config.png)

Hello 실행 계정을 선택 하면 계정 hello **속성** 창 hello 다음과 같은 오류 메시지가 표시 됩니다.

![불완전 실행 계정 구성 경고 메시지](media/automation-manage-account/automation-account-runas-incomplete-config-msg.png)에서도 확인할 수 있습니다.

삭제 및 다시 hello 계정을 작성 하 여 이러한 계정으로 실행 계정 문제를 신속 하 게 해결할 수 있습니다.

## <a name="next-steps"></a>다음 단계
* 서비스 사용자에 대 한 자세한 내용은 참조 너무[응용 프로그램 개체 및 서비스 주체 개체](../active-directory/active-directory-application-objects.md)합니다.
* Azure 자동화에서 역할 기반 액세스 제어에 대 한 자세한 내용은 참조 너무[Azure 자동화에서 역할 기반 액세스 제어](automation-role-based-access-control.md)합니다.
* 인증서 및 Azure 서비스에 대 한 자세한 내용은 참조 너무[Azure 클라우드 서비스에 대 한 인증서 개요](../cloud-services/cloud-services-certs-create.md)합니다.
