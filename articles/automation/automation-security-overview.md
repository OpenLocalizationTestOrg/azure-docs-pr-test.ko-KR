---
title: "Azure 자동화에서 aaaIntro tooauthentication | Microsoft Docs"
description: "이 문서에서는 Azure 자동화의 자동화 계정에 대 한 자동 보안 및 사용할 수 있는 hello 다른 인증 방법의 개요를 제공 합니다."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
keywords: "자동화 보안, 안전한 자동화, 자동화 인증"
ms.assetid: 4a6bc2f5-c5a2-4dfb-b10d-7950d750dee8
ms.service: automation
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/01/2017
ms.author: magoedte
ROBOTS: NOINDEX
ms.openlocfilehash: 4b4409b5be010c16f7bf00a9a0f617e3617d4663
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooauthentication-in-azure-automation"></a>Azure 자동화에서 tooauthentication 소개  
Azure 자동화 하면 tooautomate 작업 리소스에 대 한 다른 클라우드 공급자 웹 서비스 AWS (Amazon 등)와 azure에서 온-프레미스에.  Runbook tooperform 위해에서 필요한 작업을 있어야 hello 리소스에 액세스 권한을 toosecurely hello 구독 내에서 필요한 hello 최소의 권한을 가진 합니다.

표시 tooget 시작 하는 방법에 따라 hello 환경 또는 환경의 있습니다 toomanage 필요한 및이 문서는 hello 다양 한 인증 시나리오를 지 원하는 Azure 자동화에 의해 설명 합니다.  

## <a name="automation-account-overview"></a>자동화 계정 개요
Azure 자동화를 hello 처음으로 시작할 때 자동화 계정을 하나 이상 만들어야 합니다. 자동화 계정을 tooisolate에서 자동화 리소스 (runbook, 자산, 구성) hello 다른 자동화 계정에 포함 된 리소스를 사용 합니다. 자동화 계정을 tooseparate 리소스를 별도 논리적 환경으로 사용할 수 있습니다. 예를 들어 개발, 프로덕션, 온-프레미스 환경에 서로 다른 계정을 사용할 수 있습니다.  Azure 자동화 계정은 Microsoft 계정 또는 Azure 구독에서 만든 계정과 다릅니다.

각 자동화 계정의 자동화 리소스 hello 단일 Azure 지역과 연관 되어 있지만 자동화 계정은 구독에서 모든 hello 리소스를 관리할 수 있습니다. hello 주된 이유 toocreate 자동화 계정이 다른 영역에 데이터와 리소스 toobe 격리 tooa 특정 지역을 필요로 하는 정책이 있을 수는 것입니다.

> [!NOTE]
> 자동화 계정 및 hello 리소스를 포함 하는 hello Azure 포털에서에서 만들어진, hello Azure 클래식 포털에에서 액세스할 수 없습니다. 이러한 계정 또는 Windows PowerShell을 사용 하 여 해당 리소스 toomanage를 원하는 경우 hello Azure 리소스 관리자 모듈을 사용 해야 합니다.
>

모든 Azure 리소스 관리자 및 hello Azure cmdlet 사용 하 여 Azure 자동화에서 리소스에 대해 수행 하는 hello 작업 tooAzure Azure Active Directory 조직 id 자격 증명 기반 인증을 사용 하 여 인증 해야 합니다.  인증서 기반 인증 hello 원래 인증 방법을 Azure 서비스 관리 모드를 사용 하지만 복잡 한 toosetup 합니다.  Azure AD 사용자와 tooAzure 인증가 2014 toonot에 도입 된 백만 단순화 hello 프로세스 tooconfigure tooAzure 작동 하는 단일 사용자 계정으로 인증 toonon 대화형는 인증 계정 뿐만 아니라 hello 기능 지원 Azure 리소스 관리자 및 클래식 리소스입니다.   

새 자동화 계정 hello Azure 포털에서에서 만들어야 하는 경우에 현재 자동으로 생성 됩니다.

* 실행 계정에서 인증서를 Azure Active Directory에 새 서비스 사용자를 만들고 hello 참가자 역할 기반 액세스 제어 (RBAC)을 할당 하는 runbook을 사용 하 여 toomanage 리소스 관리자 리소스를 사용 합니다.
* 기본 실행 계정을 사용 하는 Azure 서비스 관리 toomanage 수 또는 runbook을 사용 하 여 클래식 리소스는는 관리 인증서를 업로드 하 여 합니다.  

역할 기반 액세스 제어 작업 tooan Azure AD 사용자 계정 및 계정으로 실행을 허용 하는 Azure 리소스 관리자 toogrant은 사용할 수 있게 하 고 해당 서비스 보안 주체를 인증 합니다.  읽으십시오 [Azure 자동화 문서에서 역할 기반 액세스 제어](automation-role-based-access-control.md) toohelp 자세한 정보에 대 한 자동화 권한 관리를 위한 모델을 개발 합니다.  

컴퓨팅 AWS에서 서비스 또는 데이터 센터에서 Hybrid Runbook Worker에서 실행 되는 Runbook 수 없는 사용 하 여 hello 동일 tooAzure 리소스를 인증 하는 runbook에 대 한 일반적으로 사용 되는 메서드.  이러한 리소스 Azure 외부에서 실행 중이 고 하므로 로컬로 액세스 하는 자동화 tooauthenticate tooresources에 정의 된 자체 보안 자격 증명 필요는 때문입니다.  

## <a name="authentication-methods"></a>인증 방법
hello 다음 표에 요약 되어 문서 설명 하는 hello와 Azure 자동화에서 지 원하는 각 환경에 대 한 hello 다른 인증 방법을 어떻게 runbook에 대 한 toosetup 인증 합니다.

| 메서드 | Environment | 문서 |
| --- | --- | --- |
| Azure AD 사용자 계정 만들기 |Azure 리소스 관리자 및 Azure 서비스 관리 |[Azure AD 사용자 계정으로 Runbook 인증](automation-create-aduser-account.md) |
| Azure 실행 계정 |Azure 리소스 관리자 |[Azure 실행 계정으로 Runbook 인증](automation-sec-configure-azure-runas-account.md) |
| Azure 클래식 실행 계정 |Azure 서비스 관리 |[Azure 실행 계정으로 Runbook 인증](automation-sec-configure-azure-runas-account.md) |
| Windows 인증 |온-프레미스 데이터 센터 |[Hybrid Runbook Worker용 Runbook 인증](automation-hybrid-runbook-worker.md) |
| AWS 자격 증명 |Amazon 웹 서비스 |[AWS(Amazon 웹 서비스)로 Runbook 인증](automation-config-aws-account.md) |
