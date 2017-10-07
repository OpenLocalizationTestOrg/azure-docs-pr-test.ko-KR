---
title: "aaaAzure 데이터 카탈로그의 필수 구성 요소 | Microsoft Docs"
description: "Azure Data Catalog 시작 tooget 필요한 hello 필수 구성 요소에 알아봅니다."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: ef497a54-dc4d-4820-b5bf-c361b64b964d
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 0c8e768e5846c61b542b746d7ad80121725a9ec7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-prerequisites"></a>Azure 데이터 카탈로그의 필수 구성 요소

Azure Data Catalog를 설정 하려면 먼저 몇 가지 care of tootake를 해야 합니다. 걱정하지 마세요. 이 프로세스는 오래 걸리지 않습니다.

## <a name="azure-subscription"></a>Azure 구독
tooset 데이터 카탈로그를 hello 소유자 또는 Azure 구독의 공동 소유자를 여야 합니다.

Azure 구독에는 데이터 카탈로그 같은 toocloud 서비스 리소스 액세스를 구성할 수 있습니다. 구독은 리소스 사용을 보고하고, 요금을 청구하고, 지불하는 방식을 제어할 수도 있습니다. 각 구독은 별도 청구 및 지불 설정을 가질 수 있으므로 부서, 프로젝트, 지사 등에 따라 다른 구독 및 계획이 있을 수 있습니다. 모든 클라우드 서비스 tooa 구독 속하고 데이터 카탈로그를 설정 하기 전에 toohave 구독 해야 합니다. toolearn 더 참조 [계정, 구독 및 관리 역할 관리](../active-directory/active-directory-assign-admin-roles.md)합니다.

## <a name="azure-active-directory"></a>Azure Active Directory
tooset 데이터 카탈로그를 있습니다 서명 해야 Azure Active Directory (Azure AD) 사용자 계정을 사용 합니다.

Azure AD 비즈니스 toomanage id 및 액세스 방법으로 hello 클라우드 및 온-프레미스에서 모두에 대 한는 쉬운 방법을 제공합니다. 사용자에 단일 로그인 tooany 클라우드에 대 한 단일 회사 또는 학교 계정의 사용할 수 있으며 온-프레미스 웹 응용 프로그램. 데이터 카탈로그는 Azure AD tooauthenticate 로그인에 사용 됩니다. toolearn 더 참조 [Azure Active Directory 란?](../active-directory/active-directory-whatis.md)합니다.

> [!NOTE]
> Hello를 사용 하 여 [Azure 포털](http://portal.azure.com/)을 서명할 수 개인 Microsoft 계정 또는 Azure Active Directory를 사용 하 여 회사 또는 학교 계정. Azure 포털 또는 hello에 중 하나를 사용 하 여 데이터 카탈로그를 tooset hello [Data Catalog 포털](http://www.azuredatacatalog.com), 개인 계정이 아닌 계정을 Azure Active Directory를 사용 하 여 로그인 해야 합니다.
>
>

## <a name="active-directory-policy-configuration"></a>Active Directory 정책 구성
Toosign toohello 데이터 원본 등록 도구에서 시도할 때 하지만 toohello Data Catalog 포털에 로그인 할 수 있는 상황이 발생할 수 있습니다, 로그인 하면 오류 메시지가 발생 합니다. Hello 회사 네트워크에서 또는 외부 hello 회사 네트워크에서 연결 때만 발생할 수 있습니다 때에이 문제가 발생할 수 있습니다.

hello 데이터 원본 등록 도구는 폼 인증 toovalidate Active Directory에 대해 사용자 자격 증명을 사용합니다. toohelp 성공적으로 로그인을 Active Directory 관리자는 hello 전역 인증 정책에서에서 폼 인증을 설정 해야 합니다.

Hello 전역 인증 정책, 인증 방법 스크린 샷 다음 hello와 같이 설정을 변경 하려면 별도로 인트라넷 및 익스트라넷 연결을 수 있습니다. 연결 중인 hello 네트워크에 대 한 폼 인증을 사용 하지 않는 경우 로그인 오류가 발생할 수 있습니다.

 ![Active Directory 전역 인증 정책](./media/data-catalog-prerequisites/global-auth-policy.png)

## <a name="next-steps"></a>다음 단계
자세한 내용은 [인증 정책 구성](https://technet.microsoft.com/library/dn486781.aspx)을 참조하세요.
