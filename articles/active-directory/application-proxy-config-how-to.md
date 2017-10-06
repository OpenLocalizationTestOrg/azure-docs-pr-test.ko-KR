---
title: "응용 프로그램 프록시 응용 프로그램 aaaHow tooconfigure | Microsoft Docs"
description: "자세한 내용은 방법 toocreate 몇 가지 간단한 단계에서는 응용 프로그램 프록시 응용 프로그램 구성"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: c64019098fc124e4fe10b8288830bcd2b7239d3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-an-application-proxy-application"></a>어떻게 tooconfigure 응용 프로그램 프록시 응용 프로그램

이 문서가 도움이 toounderstand 방법을 Azure AD tooexpose 내에서 응용 프로그램 프록시 응용 프로그램 tooconfigure 온-프레미스 응용 프로그램 toohello 클라우드입니다.

## <a name="recommended-documents"></a>권장되는 문서 

hello 초기 구성과 hello 관리자 포털을 통해 응용 프로그램 프록시 응용 프로그램 만들기에 대 한 toolearn hello에 따라 [Azure AD 응용 프로그램 프록시를 사용 하 여 응용 프로그램을 게시](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal)합니다.

커넥터를 구성 하는 방법에 대 한 세부 정보를 참조 하십시오. [hello Azure 포털에서에서 응용 프로그램 프록시를 사용 하도록 설정](active-directory-application-proxy-enable.md)합니다.

인증서 업로드 및 사용자 지정 도메인 사용에 대한 자세한 내용은 [Azure AD 응용 프로그램 프록시에서 사용자 지정 도메인 작업](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains)을 참조하세요.

## <a name="create-hello-applicationsetting-hello-urls"></a>응용 프로그램/설정 hello Url hello를 만들려면

Hello hello의 단계를 따르는 경우 [Azure AD 응용 프로그램 프록시를 사용 하 여 응용 프로그램을 게시](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal) 설명서 및가 정보에 대 한 hello 오류 세부 정보 및 방법에 대 한 제안 사항 참조 hello 응용 프로그램을 만드는 동안 오류가 발생 하기 toofix hello 응용 프로그램입니다. 대부분의 오류 메시지에는 제안 수정이 포함되어 있습니다. tooavoid 일반적인 오류를 확인 합니다.

-   관리자 권한 toocreate 응용 프로그램 프록시 응용 프로그램 사용

-   hello 내부 URL은 고유

-   hello 외부 URL이 고유

-   hello http 또는 https를 사용한 Url 시작 하 고 끝나야는 "/"

-   hello URL에 IP 주소가 아닌 도메인 이름 이어야 합니다.

hello 응용 프로그램을 만들 때 hello 오른쪽 위 모서리에 hello 오류 메시지가 표시 되어야 합니다. Hello 알림 아이콘 toosee hello 오류 메시지를 선택할 수 있습니다.

   ![알림 프롬프트](./media/application-proxy-config-how-to/error-message.png)

## <a name="configure-connectorsconnector-groups"></a>커넥터/커넥터 그룹 구성

Hello 커넥터 및 커넥터 그룹에 대 한 경고로 인해 응용 프로그램을 구성 하는 데 문제가 있는 경우 응용 프로그램 프록시를 사용 하도록 설정 방법에 대 한 세부 정보에 대 한 지침을 참조 toodownload 커넥터입니다. 커넥터에 대 한 자세한 toolearn hello를 참조 하십시오 [커넥터 설명서](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors)합니다.

커넥터를 활성 없는 경우이 없습니다 tooreach hello 서비스 되는지 의미 합니다. 종종 모든 hello 필요한 포트가 열려 있습니다. 필요한 포트 목록이 toosee 응용 프로그램 프록시 설명서를 활성화 하는 hello의 hello 필수 구성 요소 섹션을 참조 합니다.

## <a name="upload-certificates-for-custom-domains"></a>사용자 지정 도메인에 대한 인증서 업로드

사용자 지정 도메인을 사용 하면 외부 Url의 toospecify hello 도메인 있습니다. toouse 사용자 지정 도메인을 해당 도메인에 대 한 tooupload hello 인증서가 필요 합니다. 사용자 지정 도메인 및 인증서 사용에 대한 자세한 내용은 [Azure AD 응용 프로그램 프록시에서 사용자 지정 도메인 작업](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains)을 참조하세요. 

인증서를 업로드 하는 문제를 발생 하는 경우 hello 인증서 문제가 hello에 대 한 자세한 내용은 hello 포털에서 hello 오류 메시지를 찾아보십시오. 인증서의 일반적인 문제는 다음과 같습니다.

-   만료된 인증서

-   자체 서명된 인증서

-   Hello 개인 키를 인증서가 없습니다.

hello 오류 메시지에 hello 오른쪽 위 모서리 tooupload hello 인증서를 사용 하는 대로 표시 합니다. Hello 알림 아이콘 toosee hello 오류 메시지를 선택할 수 있습니다.

   ![알림 프롬프트](./media/application-proxy-config-how-to/error-message2.png)

## <a name="next-steps"></a>다음 단계
[Azure AD 응용 프로그램 프록시를 사용하여 응용 프로그램 게시](application-proxy-publish-azure-portal.md)
