---
title: "Azure Active Directory Domain Services: 시작 | Microsoft Docs"
description: "Azure Active Directory 도메인 서비스 hello Azure 포털 (미리 보기)를 사용 하 여 사용 하도록 설정"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: maheshu
ms.openlocfilehash: 8bde872a13bc9960d1e62c74017ff78a8953a0a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a>Azure Active Directory 도메인 서비스 hello Azure 포털 (미리 보기)를 사용 하 여 사용 하도록 설정


## <a name="task-3-configure-administrative-group"></a>작업 3: 관리 그룹 구성
이 구성 작업에서는 Azure AD 디렉터리에 관리 그룹을 만듭니다. 이 특수 관리 그룹을 *AAD DC Administrators*라고 합니다. 이 그룹의 구성원은 관리 되는 도메인 toohello 도메인에 가입 된 컴퓨터에 대 한 관리 권한이 부여 됩니다. 도메인에 가입 된 컴퓨터에서이 그룹은 toohello 관리자 그룹을 추가 합니다. 또한이 그룹의 구성원 원격 데스크톱 tooconnect 원격으로 toodomain에 가입 된 컴퓨터를 사용할 수 있습니다.

> [!NOTE]
> Azure Active Directory 도메인 서비스를 사용 하 여 만든 hello 관리 되는 도메인에 도메인 관리자 또는 엔터프라이즈 관리자 권한이 없는 합니다. 관리 되는 도메인에 이러한 hello 서비스에서 예약 된 사용 권한과 hello 테 넌 트 내에서 사용할 수 있는 toousers 적용 되지 않습니다. 그러나 만든 hello 특별 한 관리 그룹을 사용할 수 있습니다이 구성 작업 tooperform에서 일부 권한 있는 작업입니다. 이러한 작업 컴퓨터 toohello 도메인 가입, toohello 관리 그룹 도메인에 가입 된 컴퓨터에 속하는 및 그룹 정책 구성에 포함 됩니다.
>

hello 마법사는 자동으로 Azure AD 디렉터리의 hello 관리 그룹을 만듭니다. 이 그룹을 'AAD DC Administrators'라고 합니다. Azure AD 디렉터리에이 이름 가진 기존 그룹 했다면 hello 마법사는이 그룹을 선택 합니다. Hello를 사용 하 여 그룹 멤버 자격을 구성할 수 있습니다 **관리자 그룹** 마법사 페이지입니다.

1. tooconfigure 그룹 구성원을 클릭 하 여 **AAD DC 관리자**합니다.

    ![그룹 멤버 자격 구성](./media/getting-started/domain-services-blade-admingroup.png)

2. Hello 클릭 **멤버 추가** tooadd 사용자가 Azure AD 디렉터리 toohello 관리자 그룹에서 단추입니다.

3. 완료 되 면 클릭 **확인** toohello에 toomove **요약** hello 마법사의 페이지입니다.

4. Hello에 **요약** hello hello 관리 되는 도메인에 대 한 구성 설정 검토 hello 마법사의 페이지입니다. 돌아갈 수 있습니다 tooany 단계 hello 마법사 toomake 변경 내용이 필요한 경우. 완료 되 면 클릭 **확인** toocreate hello 새 관리 되는 도메인입니다.

    ![요약](./media/getting-started/domain-services-blade-summary.png)

5. Azure AD 도메인 서비스 배포의 실행 과정과 hello 보여 주는 알림이 표시 됩니다. Hello 알림을 클릭 toosee hello 배포에 대 한 진행률을 자세히 설명 합니다.

    ![알림 - 배포 진행 중](./media/getting-started/domain-services-blade-deployment-in-progress.png)


## <a name="provision-your-managed-domain"></a>관리되는 도메인 프로비전
관리 되는 도메인 사용자를 프로 비전의 hello 프로세스 tooan 시간을 사용할 수 있습니다.

1. 배포 진행 중에서 상태인 동안에 '도메인 서비스' hello에서 검색할 수 있습니다 **리소스 검색** 검색 상자입니다. 선택 **Azure AD 도메인 서비스** hello 검색 결과에서. hello **Azure AD 도메인 서비스** 블레이드에 프로 비전 하는 hello 관리 되는 도메인을 나열 합니다.

    ![프로비전되는 관리되는 도메인 찾기](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. Hello 도메인에 대 한 자세한 내용은 hello 관리 되는 도메인 (예를 들어 ' contoso100.com') toosee의 hello 이름을 클릭 합니다.

    ![Domain Services - 프로비저닝 상태](./media/getting-started/domain-services-provisioning-state.png)

3. hello **개요** 해당 hello 도메인이 현재 프로비저닝되 고 탭에 표시 합니다. 완전히 프로 비전 될 때까지 hello 관리 되는 도메인을 구성할 수 없습니다. 완전히 프로 비전 하 여 관리 되는 도메인 toobe tooan 시간을 걸릴 수 있습니다.

    ![도메인 서비스-hello 상태를 프로 비전 하는 동안 개요 탭 ](./media/getting-started/domain-services-provisioning-state-details.png)

4. 관리 되는 도메인 hello 완전히 프로 비전 때 hello **개요** hello 도메인 상태 탭에 표시 **실행**합니다.

    ![Domain Services - 완전히 프로비전한 후 개요 탭](./media/getting-started/domain-services-provisioned.png)

5. Hello에 **속성** hello 가상 네트워크에 사용할 수 있는 컨트롤러는 도메인에 두 개의 IP 주소가 표시 탭 합니다.

    ![Domain Services - 완전히 프로비전한 후 속성 탭](./media/getting-started/domain-services-provisioned-properties.png)


## <a name="next-step"></a>다음 단계
[작업 4: hello Azure 가상 네트워크에 대 한 hello DNS 설정을 업데이트합니다](active-directory-ds-getting-started-dns.md)
