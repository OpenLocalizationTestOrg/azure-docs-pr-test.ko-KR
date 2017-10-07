---
title: "Azure 구독 aaaUse Office 365 테 넌 트 | Microsoft Docs"
description: "자세한 내용은 방법 tooadd Office 365 디렉터리 (테 넌 트) tooan Azure 구독."
services: 
documentationcenter: 
author: JiangChen79
manager: jlian
editor: 
tags: billing,top-support-issue
ms.assetid: cc9c57c6-7bfd-4dea-9027-c75ef3737589
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: cjiang
ms.openlocfilehash: e560370417bd074a7e37ceb7c60da45dbbbcf775
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="associate-an-office-365-tenant-tooan-azure-subscription"></a>Office 365 테 넌 트 tooan Azure 구독 연결
Azure 구독에서 hello Office 365 테 넌 트에 액세스할 수 있도록 별도 Azure 및 Office 365 구독을 연결 합니다. toolink tooAzure hello Azure 서비스 관리자 계정으로 로그인 구독 디렉터리를 추가 하 고 hello Office 365 조직 계정 toohello Azure Active Directory 테 넌 트를 추가 합니다.

Azure Active Directory 인스턴스에서 사용자를 위한 Office 365 구독이 필요하거나 Office 365 계정이 있지만 Azure 계정이 없는 경우 [Office 365 계정을 사용하여 Azure에 등록](billing-use-existing-office-365-account-azure-subscription.md)을 참조하세요. 

## <a name="before-you-begin"></a>시작하기 전에
* Azure 구독의 서비스 관리자에 게의 hello 자격 증명이 있어야 합니다. 공동 관리자 계정에이 문서의 hello 단계 중 일부를 수행할 수 없습니다. toochange 서비스 관리자에 게 참조 [어떻게 tooadd 또는 변경 Azure 관리자 역할](billing-add-change-azure-subscription-administrator.md#change-service-administrator-for-a-subscription)합니다.
* Hello Office 365 테 넌 트의 전역 관리자의 hello 자격 증명이 있어야 합니다.
* hello Office 365 테 넌 트에 서비스 관리자에 게의 hello 전자 메일 주소 수 없습니다.
* 서비스 관리자에 게 전자 메일 주소 hello hello Office 365 테 넌 트의 전역 관리자의 같아야 합니다.
* Microsoft 계정과 조직 계정 되는 전자 메일 주소를 사용 하는 경우 일시적으로 변경의 Azure 구독 toouse 서비스 관리자에 게 다른 Microsoft 계정. Hello에서 Microsoft 계정을 만들 수 있습니다 [Microsoft 계정 등록 페이지로](https://signup.live.com/)합니다.

## <a name="link-office-365-tenant-tooazure-subscription"></a>Office 365 테 넌 트 tooAzure 구독 연결
tooassociate hello Office 365 테 넌 트 toohello Azure 구독에는 다음이 단계를 따르십시오.

### <a name="step-1-add-office-365-tenant-tooyour-azure-subscription"></a>1 단계: Office 365 테 넌 트 tooyour Azure 구독 추가

1. Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com/) hello 서비스 관리자 자격 증명을 사용 합니다.

    ![Azure 로그인의 스크린샷](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)

2. Hello 왼쪽된 창에서 선택 **ACTIVE DIRECTORY**합니다. Hello Office 365 테 넌 트를 참조 하지 않아야 합니다. 표시, 경우 너무 건너뛸[2 단계: Azure 구독 hello와 관련 된 hello 디렉터리를 변경](#Step2)합니다.
   
   ![Active Directory 항목의 스크린샷](./media/billing-add-office-365-tenant-to-azure-subscription/s35-classic-portal-active-directory-entry.png)

3. **새로 만들기** > **디렉터리** > **사용자 지정 만들기**를 선택합니다.
   
    ![Azure Active Directory 사용자 지정 만들기의 스크린샷](./media/billing-add-office-365-tenant-to-azure-subscription/s37-aad-custom-create.png)
   
4. Hello에 **디렉터리 추가** 페이지의 **디렉터리**선택, **기존 디렉터리를 사용 하 여**합니다. 다음 선택 **지금 로그 아웃 준비 toobe 저는**를 선택 하 고 **완료** ![완료 아이콘](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png)합니다.
   
    !["기존 디렉터리 사용"의 스크린샷](./media/billing-add-office-365-tenant-to-azure-subscription/s39_add-directory-use-existing.png)
   
5. 로그 아웃, Office 365 테 넌 트의 hello 전역 관리자 자격 증명을 사용 하 여 로그인 합니다.
   
    ![Office 365 전역 관리자 로그인의 스크린샷](./media/billing-add-office-365-tenant-to-azure-subscription/s310_sign-in-global-admin-office-365.png)
   
6. **계속**을 선택합니다.
   
    ![확인의 스크린샷](./media/billing-add-office-365-tenant-to-azure-subscription/s311_use-contoso-directory-azure-verify.png)
   
7. **지금 로그아웃**을 선택합니다.
   
    ![로그아웃의 스크린샷](./media/billing-add-office-365-tenant-to-azure-subscription/s312_use-contoso-directory-azure-confirm-and-sign-out.png)
   
8. Toohello 로그인 [Azure 클래식 포털](https://manage.windowsazure.com/) hello 서비스 관리자 자격 증명을 사용 합니다.
   
    ![Azure 로그인의 스크린샷](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)
   
9. Hello 대시보드에서 Office 365 테 넌 트에 대해 표시 됩니다.
   
    ![대시보드의 스크린샷](./media/billing-add-office-365-tenant-to-azure-subscription/s314_office-365-tenant-appear-in-azure.png)

### <a name="Step2"></a>2 단계: Azure 구독 hello와 연관 된 hello 디렉터리 변경
   
1. **설정**을 선택합니다.
   
    ![Azure 클래식 포털 설정 아이콘의 스크린샷](./media/billing-add-office-365-tenant-to-azure-subscription/s315_azure-classic-portal-settings-icon.png)
   
2. Azure 구독을 선택한 다음 **디렉터리 편집**을 선택합니다.

    ![Azure 구독 편집 디렉터리의 스크린샷](./media/billing-add-office-365-tenant-to-azure-subscription/s316_azure-subscription-edit-directory.png)
   
3. **다음** ![다음 아이콘](./media/billing-add-office-365-tenant-to-azure-subscription/s317_next-icon.png)을 선택합니다.
   
    !["변경 관련된 디렉터리를 hello"의 스크린 샷](./media/billing-add-office-365-tenant-to-azure-subscription/s318_azure-change-associated-directory.png)
   
4. 영향을 받는 hello 계정을 검토 합니다. 모든 공동 관리자와 [역할 기반 액세스 제어 (RBAC)](../active-directory/role-based-access-control-configure.md) hello 기존 리소스 그룹에 할당 된 액세스 권한이 있는 사용자가 제거 됩니다. 만 표시 될 hello 경고 공동 관리자의 hello 제거에 언급 합니다.
      
    ![공동 관리자 계정 toobe 제거 hello를 보여 주는 스크린 샷](./media/billing-add-office-365-tenant-to-azure-subscription/s322_azure-confirm-directory-mapping.png)
   
    ![제거 하는 예에서는 사용자 계정 toobe 보여 주는 스크린 샷](./media/billing-add-office-365-tenant-to-azure-subscription/s325_assigned-users-removed-resource-groups.png)
   
5. **완료** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png)을 선택합니다.

### <a name="step-3-add-your-office-365-organizational-accounts-as-co-administrators-toohello-azure-active-directory-tenant"></a>3 단계: 공동 관리자 toohello Azure Active Directory 테 넌 트로 Office 365 조직 계정 추가
   
1. 선택 hello **관리자** 탭을 선택한 다음 선택 **추가**합니다.
   
    ![Azure 클래식 포털 설정 관리자 탭의 스크린샷](./media/billing-add-office-365-tenant-to-azure-subscription/s319_azure-classic-portal-settings-administrators.png)
   
2. Office 365 테 넌 트의 조직 계정을 입력 hello Azure 구독을 선택한 다음 선택 **완료** ![완료 아이콘](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png)합니다.
   
    ![Azure 공동 관리자 추가 대화 상자의 스크린샷](./media/billing-add-office-365-tenant-to-azure-subscription/s320_azure-add-co-administrator.png)
   
3. Toohello 돌아가서 **관리자** 탭 합니다. Hello 조직 계정을 공동 관리자로 표시 표시 되어야 합니다.
   
    ![관리자 탭의 스크린샷](./media/billing-add-office-365-tenant-to-azure-subscription/s321_azure-co-administrator-added.png)
4.  액세스 tooAzure hello 공동 관리자 계정으로 테스트 합니다.
   
    a. 로그 아웃 hello Azure 클래식 포털.
   
    b. 열기 hello [Azure 포털](https://portal.azure.com/)합니다.
   
    c. 공동 관리자에 게의 hello 자격 증명을 입력 한 다음 선택 **로그인**합니다.
   
    ![Azure 로그인 페이지의 스크린샷](./media/billing-add-office-365-tenant-to-azure-subscription/s324_azure-sign-in-with-co-admin.png)

## <a name="need-help-contact-support"></a>도움이 필요하세요? 지원에 문의하세요.
도움이 필요 하면 여전히 필요 하면 [지원에 문의](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget 문제가 해결 신속 하 게 합니다.


