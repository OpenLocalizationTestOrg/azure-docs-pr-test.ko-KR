---
title: "Azure AD 테 넌 트 aaaHow tooget | Microsoft Docs"
description: "어떻게 tooget Azure Active Directory 등록 응용 프로그램을 구축 하기 위한 테 넌 트."
services: active-directory
documentationcenter: 
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 1f4b24eb-ab4d-4baa-a717-2a0e5b8d27cd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/19/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: dcc6b3109528cf763bda9bd527344ea9ab5c0d69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-an-azure-active-directory-tenant"></a>Tooget Azure Active Directory 테 넌 트
Azure Active Directory (Azure AD)에서 [테넌트](https://msdn.microsoft.com/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant) 는 조직을 나타냅니다.  것은 hello 조직 수신 하 고 Azure, Microsoft Intune 또는 Office 365 같은 Microsoft 클라우드 서비스에 등록 하는 경우를 소유 하는 Azure AD 서비스의 전용된 인스턴스입니다.  각 Azure AD 테넌트는 서로 전혀 다르고 다른 Azure AD 테넌트와 별개입니다.  

테 넌 트에 대 한-암호, 사용자 프로필 데이터, 권한 및 등 회사 및 hello 정보 hello 사용자가 보관합니다.  또한 그룹, 응용 프로그램 및 tooan 조직 및 보안 관련 된 기타 정보를 포함 합니다.

tooyour 응용 프로그램에서 Azure AD 사용자가 toosign tooallow, 자신만의 테 넌 트에 응용 프로그램을 등록 해야 합니다.  Azure AD 테넌트에 응용 프로그램을 게시하는 것은 **무료**입니다.  사실 대부분의 개발자는 실험, 개발, 준비 및 테스트 목적으로 여러 개의 테넌트를 만듭니다.  필요에 따라 조직에 등록 하 고 응용 프로그램을 사용 하는 수 tootake 고급 디렉터리 기능을 활용 하려는 경우 toopurchase 라이선스를 선택 해야 합니다.

그럼 Azure AD 테넌트 가져오기를 시작해볼까요?  hello 프로세스를 수 있습니다 약간 다른 경우에는 있습니다.

* [기존 Office 365 구독이 있는 경우](#use-an-existing-office-365-subscription)
* [Microsoft 계정에 연결된 기존 Azure 구독이 있는 경우](#use-an-msa-azure-subscription)
* [조직 계정에 연결된 기존 Azure 구독이 있는 경우](#use-an-organizational-azure-subscription)
* [처음부터 toostart & 하나도 위의 hello 포함](#start-from-scratch)

## <a name="use-an-existing-office-365-subscription"></a>기존 Office 365 구독 사용
기존 Office 365 구독이 있는 경우 이미 Azure AD 테넌트가 있습니다. Toohello에 로그인 하려면 [Azure 포털](https://portal.azure.com) O365 계정 및 Azure AD를 사용 하 여 시작 합니다.

## <a name="use-an-msa-azure-subscription"></a>MSA Azure 구독 사용
이전에 개인 Microsoft 계정으로 Azure 구독을 등록했으면 이미 테넌트를 가지고 있습니다.  Toohello에 로그인 할 때 [Azure 포털](https://portal.azure.com), tooyour 기본 테 넌 트에 자동으로 로그인 됩니다. -맞게 때이 테 넌이 트 참조 무료 toouse 있더라도 toocreate 조직 관리자 계정을 사용할 수 있습니다.

따라서 toodo 다음이 단계를 수행 합니다.  또는 toocreate 새 테 넌 트를 원하는 하 고 비슷한 프로세스에 해당 테 넌 트의 관리자를 만들 수 있습니다.

1. Hello에 로그인 [Azure 포털](https://portal.azure.com) 개별 계정을 사용 하 여
2. 이동 hello 포털의 toohello "Azure Active Directory" 섹션 (아래에서 hello 왼쪽된 탐색 모음에서 발견 **더 서비스**)
3. "기본 디렉터리" toohello로 자동으로 로그인 될 해야 있습니다 없으면 hello 오른쪽 위 모퉁이에서 계정 이름을 클릭 하 여 디렉터리를 전환할 수 있습니다.
4. Hello에서 **빠른 작업** 섹션에서 선택 **사용자 추가**합니다.
5. 추가 사용자 양식 hello 하 hello 다음 세부 정보를 제공 합니다.

   * 이름: (적절한 값 선택)
   * 사용자 이름: (이 관리자의 사용자 이름 선택)
   * 프로필: (이름, 마지막 이름, 직함 및 부서에 대 한 hello 적절 한 값을 입력)
   * 역할: 전역 관리자 
6. 완료 했을 때 사용자 양식을 추가 hello 및 hello hello 새 관리자에 대 한 임시 암호를 수신, 순서 toochange hello 암호에이 새 사용자와 toologin 필요 하므로이 암호 있는지 toorecord 수입니다. Hello 암호를 보낼 수도 있습니다 직접 toohello 사용자를 대체 전자 메일을 사용 하 여 합니다.
7. 클릭 **만들기** toocreate hello에 대 한 새 사용자입니다.
8. toochange hello 임시 암호에 로그인 [https://login.microsoftonline.com](https://login.microsoftonline.com) 이 새 사용자와 계정 및 요청 시 hello 암호를 변경 합니다.

## <a name="use-an-organizational-azure-subscription"></a>조직 Azure 구독 사용
이전에 조직 계정으로 Azure 구독을 등록했으면 이미 테넌트를 가지고 있습니다.  Hello에 [Azure 포털](https://portal.azure.com), 너무 탐색할 때 테 넌 트를 찾아야 "더 서비스" 및 "Azure Active Directory."  이 테 넌이 트 나와 있는 것 처럼 맞게 무료 toouse 됩니다.

## <a name="start-from-scratch"></a>처음부터 시작
알 수 없는 tooyou hello 위의 모든 경우 걱정 하지 마십시오.  방문 [https://account.windowsazure.com/organization](https://account.windowsazure.com/organization) 새 조직으로 Azure에 대해 toosign 합니다.  Hello 프로세스를 완료 했으면 매우 자신의 Azure AD 테 넌 트를 서명 하는 동안 선택한 hello 도메인 이름 사용 해야 합니다.  Hello에 [Azure 포털](https://portal.azure.com), 너무 이동 하 여 테 넌 트를 찾을 수 있습니다 "에서 Azure Active Directory" hello 왼쪽 nav.

Azure에 등록 hello 과정의 일환으로, 필수 tooprovide 신용 카드 정보 수 있습니다.  믿고 진행할 수 있습니다. Azure AD에서의 응용 프로그램 게시 및 새 테넌트 만들기에 대한 비용은 청구되지 않습니다.
