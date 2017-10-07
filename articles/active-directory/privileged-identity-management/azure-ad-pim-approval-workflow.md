---
title: "aaaAzure Privileged Identity Management 승인 워크플로 | Microsoft Docs"
description: "PIM(Privileged Identity Management)의 승인 워크플로에 대해 알아봅니다."
services: active-directory
documentationcenter: 
author: barclayn
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/28/2017
ms.author: barclayn
ms.custom: pim
ms.openlocfilehash: 4afaf5c138798a803eb3d3b7905b9361d65792cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="approvals-preview"></a>승인(미리 보기)

## <a name="overview"></a>개요

Privileged Identity Management에 대 한 승인, 정품 인증에 대 한 역할 toorequire 승인을 구성 하 고 사용자 또는 그룹을 하나 또는 여러 개의 위임 된 승인자를 선택 사용할 수 있습니다. 계속 읽습니다. toolearn 어떻게 tooconfigure 역할 승인자를 선택 합니다.

>[!NOTE]
이 기능은 아직 개발 중이므로 버그가 발생할 수 있음에 유의하세요. hello 기능 명명 규칙 및 텍스트를 포함 하 여 변경 될 수 하 고 최종 고려 하지 않아야 합니다.


## <a name="key-terminology"></a>주요 용어

*적합 한 사용자 역할* – 적격 역할 사용자가 적격으로 tooan Azure AD 역할 할당 된 조직 내 사용자 (역할 활성화를 필요).

*위임된 승인자* – 역할 활성화 요청에 대한 승인을 담당하는 Azure AD 내 하나 이상의 개인 또는 그룹입니다.

## <a name="scenarios"></a>시나리오

비공개 미리 보기의 hello hello 다음 시나리오를 지원 합니다.

**PRA(권한 있는 역할 관리자)는 다음을 수행할 수 있습니다.**

-   [특정 역할에 대한 승인을 사용하도록 설정](#enable-approval-for-specific-roles)

-   [승인자가 사용자 및/또는 그룹 tooapprove 요청을 지정 합니다.](#specify-approver-users-and/or-groups-to-approve-requests)

-   [모든 권한 있는 역할에 대한 요청 및 승인 기록 보기](#view-request-and-approval-history-for-all-privileged-roles)

**지정된 승인자는 다음을 수행할 수 있습니다.**

-   [보류 중인 승인(요청) 보기](#view-pending-approvals-requests)

-   [역할 상승 요청(단일 및/또는 대량) 승인 또는 거부](#approve-or-reject-requests-for-role-elevation-single-and/or-bulk)

-   [승인/거부에 대한 근거 제공](#provide-justification-for-my-approval/rejection) 

**적격 역할 사용자는 다음을 수행할 수 있습니다.**

-   [승인이 필요한 역할의 활성화 요청](#request-activation-of-a-role-that-requires-approval)

-   [요청 tooactivate의 hello 상태 보기](#view-the-status-of-your-request-to-activate)

-   [활성화가 승인되면 Azure AD에서 작업 수행](#complete-your-task-in-azure-ad-if-activation-was-approved)

### <a name="navigation"></a>탐색

Hello 탐색 toosupport 승인 업데이트 했습니다.

![](media/azure-ad-pim-approval-workflow/image001.png)

기본 방문 페이지 hello PIM 및 hello 새 승인 설명서에 대 한 편리한 액세스 tooinformation를 제공합니다.

![](media/azure-ad-pim-approval-workflow/image002.png)

또한 PIM의 모든 사용자를 위해 새로운 섹션, 즉 '내 감사 기록'을 추가했습니다. 다음 모든 hello 정보 관련 tooyour identity를 찾을 수 있습니다. 여기에 모든 보류 중 및 완료 된 요청을 해결 하는 hello 요청에 대 한 내용을 결정 한 사항을, 지난 모든 역할 활성화에서 편리 합니다.

![](media/azure-ad-pim-approval-workflow/image003.png)

### <a name="enable-approval-for-specific-roles"></a>특정 역할에 대한 승인을 사용하도록 설정

특정 역할에 대 한 승인을 tooenable hello 왼쪽된 창에서 디렉터리 역할을 먼저 선택 합니다.

![](media/azure-ad-pim-approval-workflow/image004.png)

Hello 왼쪽된 탐색 디렉터리 역할의에서 설정을 선택 합니다.

![](media/azure-ad-pim-approval-workflow/image006.png)

[권한 있는 역할]을 선택합니다.

![](media/azure-ad-pim-approval-workflow/image009.png)

Hello에 "사용" 선택 섹션 승인 필요:

![](media/azure-ad-pim-approval-workflow/image011.png)

활성화 되 면 hello 블레이드 tooshow hello 다음 세부 정보를 확장 됩니다.

![](media/azure-ad-pim-approval-workflow/image013.png)

>[!NOTE]
모든 승인자를 지정 하지 않으려면 hello PRA(s) hello 기본 승인자가 됩니다. 이 역할에 대 한 모든 정품 인증 요청 필요한 tooapprove PRA(s) 수 있습니다.

### <a name="specify-approver-users-andor-groups-tooapprove-requests"></a>승인자가 사용자 및/또는 그룹 tooapprove 요청을 지정 합니다.

toodelegate 승인 hello 옵션 클릭 너무 "Select 승인자":

![](media/azure-ad-pim-approval-workflow/image015.png)

Hello 선택 승인자 블레이드가 로드 될 때에 특정 사용자 또는 hello 맨 위 또는 hello 미리 채워진된 목록에서 선택에 hello 검색 표시줄을 사용 하 여 그룹에 대 한 검색 후 완료 되 면 "선택"을 클릭 수 있습니다 있습니다.

![](media/azure-ad-pim-approval-workflow/image017.png)

참고: 한 번에 여러 사용자 또는 그룹을 선택할 수 있습니다.

선택 항목은 아래와 같이 선택한 승인자 hello 목록에 표시 됩니다.

![](media/azure-ad-pim-approval-workflow/image019.png)

승인자 tooremove hello 제거 단추 다음 tootheir 이름을 클릭 하면 됩니다.

tooadd 추가 승인자 반복 hello 프로세스입니다.

## <a name="view-request-and-approval-history-for-all-privileged-roles"></a>모든 권한 있는 역할에 대한 요청 및 승인 기록 보기

모든 권한 있는 역할에 대 한 요청 및 승인 기록을 tooview hello 대시보드에서 감사 내역을 선택 합니다.

![](media/azure-ad-pim-approval-workflow/image021.png)

>[!NOTE]
작업을 통해 hello 데이터를 정렬 하 고 "활성화 Approved"에 대 한 확인 수 있습니다.

### <a name="view-pending-approvals-requests"></a>보류 중인 승인(요청) 보기

요청 승인이 보류 중일 때는 위임된 승인자가 전자 메일 알림을 받게 됩니다. tooview hello (hello 새 탐색)에서 대시보드 선택 hello "보류 중인 승인 요청이" 탭에서 hello PIM 포털에서 이러한 요청 왼쪽 탐색 모음입니다.

![](media/azure-ad-pim-approval-workflow/image023.png)

여기에서 승인 보류 중인 요청 목록이 표시됩니다.

![](media/azure-ad-pim-approval-workflow/image024.png)

### <a name="approve-or-reject-requests-for-role-elevation-single-andor-bulk"></a>역할 상승 요청(단일 및/또는 대량) 승인 또는 거부

Hello 요청 tooapprove 원하는 또는 거부, 선택한 hello 결정 하는 데와 일치 하는 작업 모음 단추를 클릭 합니다.

![](media/azure-ad-pim-approval-workflow/image025.png)

### <a name="provide-justification-for-my-approvalrejection"></a>승인/거부에 대한 근거 제공

새 블레이드 tooapprove 열 되거나 한 번에 여러 개의 요청을 거부 됩니다. 프로그램 의사 결정에 대 한 근거를 입력 하 고 클릭 승인 (또는 거부) hello 아래쪽 또는 hello 블레이드에서:

![](media/azure-ad-pim-approval-workflow/image029.png)

Hello 요청 프로세스를 완료 하는 경우 상태 기호가 hello 결정 하면를 반영 합니다 (이 예제에서는 hello 의사 결정은 승인):

![](media/azure-ad-pim-approval-workflow/image031.png)

### <a name="request-activation-of-a-role-that-requires-approval"></a>승인이 필요한 역할의 활성화 요청

승인 hello 이전 하는 PIM 탐색 또는 hello 새 탐색에서 시작할 수 있습니다 필요한 역할의 활성화를 요청, 역할 활성화 상태로 유지 됩니다에 대 한 hello 프로세스로 hello 동일 합니다. 활성화 하는 역할의 hello 목록에서 역할을 선택 하기만 하면:

![](media/azure-ad-pim-approval-workflow/image033.png)

권한 있는 역할에 Multi-Factor Authentication이 필요한 경우 먼저 해당 작업을 완료하도록 요구하는 메시지가 표시됩니다.

![](media/azure-ad-pim-approval-workflow/image035.png)

해당 작업이 완료되면 [활성화]를 클릭하고 필요에 따라 근거를 제공합니다.

![](media/azure-ad-pim-approval-workflow/image037.png)

요청 hello 알림을 승인 보류 중입니다 hello 요청자에 게 표시 됩니다.

![](media/azure-ad-pim-approval-workflow/image039.png)

### <a name="view-hello-status-of-your-request-tooactivate"></a>요청 tooactivate의 hello 상태 보기

보류 중인 요청 tooactivate hello 상태 보기에서 새 탐색 액세스 해야 합니다. Hello 왼쪽된 탐색 모음에서 hello "내 요청" 탭을 선택 합니다.

![](media/azure-ad-pim-approval-workflow/image041.png)

hello 요청 상태 "보류 중", 너무 기본적으로 모든 toosee 설정/해제할 수 있지만 또는 요청을 거부 합니다.

### <a name="complete-your-task-in-azure-ad-if-activation-was-approved"></a>활성화가 승인되면 Azure AD에서 작업 수행

Hello 요청이 승인 되 면 hello 역할 활성 상태 이며이 역할을 필요로 하는 작업을 진행할 수 있습니다.

![](media/azure-ad-pim-approval-workflow/image043.png)

## <a name="next-steps"></a>다음 단계

사용자 의견은 중요 한 toous 합니다. 언제 라도 무료 tooshare 의견 또는 피드백와 체결 여기!
