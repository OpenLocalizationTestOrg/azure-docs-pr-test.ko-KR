---
title: "aaaFederating 단일 AD FS와 함께 여러 Azure AD | Microsoft Docs"
description: "이 문서에서는 살펴보겠습니다 어떻게 toofederate 단일 AD FS와 함께 여러 Azure AD."
keywords: "페더레이션, ADFS, AD FS, 다중 테넌트, 단일 AD FS, 단일 ADFS, 다중 테넌트 페더레이션, 다중 포리스트 ADFS, AAD 연결, 페더레이션, 테넌트 간 페더레이션"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: anandy; billmath
ms.openlocfilehash: 442192896b3b13f7bf9388396cd3769e194329d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
#<a name="federate-multiple-instances-of-azure-ad-with-single-instance-of-ad-fs"></a>AD FS의 단일 인스턴스를 사용하여 Azure AD의 여러 인스턴스를 페더레이션

양방향 트러스트가 있는 경우 하나의 고가용성 AD FS 팜에서 여러 포리스트를 페더레이션할 수 있습니다. 이러한 다중 포리스트 수도 toohello과 일치 하지 않게 동일한 Azure Active Directory 합니다. 이 문서는 단일 AD FS 배포를 여러 개 사이의 tooconfigure 페더레이션 해당 동기화 toodifferent Azure AD 포리스트 하는 방법에 지침을 제공 합니다.

![단일 AD FS로 다중 테넌트 페더레이션](media/active-directory-aadconnectfed-single-adfs-multitenant-federation/concept.png)
 
> [!NOTE]
> 이 시나리오에서는 장치 쓰기 저장 및 자동 장치 연결이 지원되지 않습니다.

> [!NOTE]
> Azure AD Connect Azure AD Connect 단일 Azure AD에서 도메인에 대 한 페더레이션의 구성할 수 있습니다이 시나리오에서 사용 되는 tooconfigure 페더레이션 수 없습니다.

##<a name="steps-for-federating-ad-fs-with-multiple-azure-ad"></a>여러 Azure AD를 사용하여 AD FS를 페더레이션하는 단계

에 Azure Active Directory contoso.onmicrosoft.com 도메인 contoso.com hello AD FS 온-프레미스 contoso.com 온-프레미스 Active Directory 환경에 설치 된 이미 페더레이션 되는 것이 좋습니다. fabrikam.com은 fabrikam.onmicrosoft.com Azure Active Directory의 도메인입니다.

##<a name="step-1-establish-a-two-way-trust"></a>1단계: 양방향 트러스트 설정
 
Fabrikam.com의 toobe 수 tooauthenticate 사용자가 contoso.com의 AD FS를 contoso.com과 fabrikam.com을 간에 양방향 트러스트가 필요 합니다. 이 hello 지침에 따라 [문서](https://technet.microsoft.com/library/cc816590.aspx) toocreate hello 양방향 트러스트 합니다.
 
##<a name="step-2-modify-contosocom-federation-settings"></a>2단계: contoso.com 페더레이션 설정 수정 
 
hello 기본 발급자가 페더레이션 되는 단일 도메인 tooAD FS "http://ADFSServiceFQDN/adfs/services/trust", 예를 들어 "http://fs.contoso.com/adfs/services/trust"에 대 한 설정입니다. Azure Active Directory에는 각 페더레이션 도메인마다 고유한 발급자가 필요합니다. Hello 동일한 AD FS는 toofederate 두 도메인에서 한 걸음 hello 발급자 값 필요 toobe AD FS는 Azure Active Directory와 페더레이션 하는 각 도메인에 대해 고유 하 게 수정 합니다. 
 
Hello AD FS 서버에서 Azure AD PowerShell을 열고 hello 다음 단계를 수행 합니다.
 
연결 설정을 포함 하는 hello 도메인 contoso.com Connect-msolservice 업데이트 hello 페더레이션 contoso.com Update-msolfederateddomain-DomainName contoso.com에 대 한 Azure Active Directory toohello – SupportMultipleDomain
 
Hello 도메인 페더레이션 설정에서 발급자는 변경 너무 "http://contoso.com/adfs/services/trust"는 발급 클레임 hello Azure AD 신뢰 당사자 트러스트 tooissue hello issuerId 값 hello UPN 접미사에 따라 올바른 규칙으로 추가 됩니다.
 
##<a name="step-3-federate-fabrikamcom-with-ad-fs"></a>3단계: AD FS로 fabrikam.com 페더레이션
 
Azure AD powershell에서 세션을 수행할 단계를 수행 하는 hello: tooAzure hello 도메인 fabrikam.com을 포함 하는 Active Directory 연결

    Connect-MsolService
관리 되는 fabrikam.com 도메인 toofederated hello를 변환 합니다.

    Convert-MsolDomainToFederated -DomainName anandmsft.com -Verbose -SupportMultipleDomain
 
작업 위에 hello에서 hello 도메인 fabrikam.com hello 동일한 AD FS와 페더레이션 합니다. 두 도메인 모두에 대 한 Get-msoldomainfederationsettings를 사용 하 여 hello 도메인 설정을 확인할 수 있습니다.

## <a name="next-steps"></a>다음 단계
[Active Directory와 Azure Active Directory 연결](active-directory-aadconnect.md)
