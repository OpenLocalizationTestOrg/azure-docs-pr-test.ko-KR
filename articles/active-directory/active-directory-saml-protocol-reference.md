---
title: "AD SAML 프로토콜 참조 aaaAzure | Microsoft Docs"
description: "이 문서에서는 Azure Active Directory에서 Single Sign-on 및 Single Sign-Out SAML 프로필 hello에 대 한 개요를 제공 합니다."
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.assetid: 88125cfc-45c1-448b-9903-a629d8f31b01
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: priyamo
ms.openlocfilehash: d540b8cd9352e3196a0f4a40f0070d0e61127bee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# Azure Active Directory hello SAML 프로토콜을 사용 하는 방법
Azure Active Directory (Azure AD) 사용 하 여 hello SAML 2.0 프로토콜 tooenable 응용 프로그램 tooprovide single sign-on 경험 tootheir 사용자입니다. hello [Single Sign On](active-directory-single-sign-on-protocol-reference.md) 및 [Single Sign-Out](active-directory-single-sign-out-protocol-reference.md) SAML 어설션, 프로토콜 및 바인딩이에서 어떻게 사용 되는지를 hello id 공급자 서비스의 Azure AD SAML 프로필에 설명 합니다.

SAML 프로토콜 hello id 공급자 (Azure AD)와 hello 서비스 공급자 (hello 응용 프로그램) tooexchange 자신에 대 한 정보를 요구합니다.

응용 프로그램이 Azure AD에 등록 될 hello 응용 프로그램 개발자 에게도 Azure AD와 페더레이션 관련 정보를 등록 합니다. 여기에 hello **리디렉션 URI** hello 응용 프로그램의 합니다.

Azure Active Directory는 테넌트별 및 공통(테넌트 독립적) single sign-on 및 single sign-out 끝점을 노출합니다. 이러한 Url 위치를 주소 지정 가능한 나타냅니다-없는 단순한 식별자 toohello 끝점 tooread hello 메타 데이터를 이동할 수 있도록 합니다.

* hello 테 넌 트 별 끝점은에 `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`합니다.  hello <TenantDomainName> 자리 표시자는 등록 된 도메인 이름 또는 Azure AD 테 넌 트의 TenantID GUID를 나타냅니다. 예를 들어 hello contoso.com 테 넌 트의 hello 페더레이션 메타 데이터를: https://login.microsoftonline.com/contoso.com/FederationMetadata/2007-06/FederationMetadata.xml

* hello 테 넌 트 독립적 끝점은에 `https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml`합니다. 이 끝점 주소에 **일반적인** 테 넌 트 도메인 이름 또는 id입니다. 대신 표시

Azure AD에 게시 하는 hello 페더레이션 메타 데이터 문서에 대 한 정보를 참조 하십시오. [페더레이션 메타 데이터](active-directory-federation-metadata.md)합니다.
