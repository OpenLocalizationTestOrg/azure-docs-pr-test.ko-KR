---
title: "인증서를 사용 하 여 Azure AD Reporting API hello aaaGet 데이터를 사용 하 여 | Microsoft Docs"
description: "Toouse 사용자 개입 없이 디렉터리에서 인증서 자격 증명 tooget 데이터를 사용 하 여 Azure AD Reporting API hello 하는 방법에 대해 설명 합니다."
services: active-directory
documentationcenter: 
author: ramical
writer: v-lorisc
manager: kannar
ms.assetid: 
ms.service: active-directory
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/24/2017
ms.author: ramical
ms.openlocfilehash: 00ddfaefe32ea6ae48f276c974a17ddcf84f7894
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-data-using-hello-azure-ad-reporting-api-with-certificates"></a>인증서가 있는 hello Azure AD Reporting API를 사용 하 여 데이터 가져오기
이 문서에서는 toouse 사용자 개입 없이 디렉터리에서 인증서 자격 증명 tooget 데이터를 사용 하 여 Azure AD Reporting API hello 하는 방법을 설명 합니다. 

## <a name="use-hello-azure-ad-reporting-api"></a>사용 하 여 Azure AD Reporting API hello 
Azure AD Reporting API 단계를 수행 하는 hello를 완료 해야 합니다.
 *  필수 구성 요소 설치
 *  응용 프로그램에서 hello 인증서를 설정 합니다.
 *  액세스 토큰 가져오기
 *  Hello 액세스 토큰 toocall hello Graph API를 사용 하 여

원본 코드에 대한 정보는 [보고서 API 모듈 활용](https://github.com/AzureAD/azure-activedirectory-powershell/tree/gh-pages/Modules/AzureADUtils)을 참조하세요. 

### <a name="install-prerequisites"></a>필수 구성 요소 설치
Azure AD PowerShell V2 toohave 및 AzureADUtils 모듈을 설치 해야 합니다.

1. 다운로드 하 여 Azure AD Powershell V2, hello 지침에 따라 설치 [Azure Active Directory PowerShell](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure AD Cmdlets/AzureAD/index.md)합니다.
2. hello Azure AD 유틸리티 모듈 다운로드 [azure Ad/azure-active directory powershell](https://github.com/AzureAD/azure-activedirectory-powershell/blob/gh-pages/Modules/AzureADUtils/AzureADUtils.psm1)합니다. 
  이 모듈에서는 다음을 비롯한 몇 가지 유틸리티 cmdlet을 제공합니다.
   * hello Nuget을 사용 하 여 ADAL의 최신 버전
   * ADAL을 사용하는 사용자, 응용 프로그램 키 및 인증서의 액세스 토큰
   * Graph API를 처리하는 페이지 단위의 결과

**tooinstall hello Azure AD 유틸리티 모듈:**

1. 디렉터리 toosave hello 유틸리티 모듈 (예를 들어 c:\azureAD)을 만들고 GitHub에서 hello 모듈을 다운로드 합니다.
2. PowerShell 세션을 열고 방금 만든 toohello 디렉터리를 이동 합니다. 
3. Hello 모듈 가져오기 및 설치 AzureADUtilsModule hello cmdlet를 사용 하 여 hello PowerShell 모듈 경로에 설치 합니다. 

hello 세션은 유사한 toothis 화면 표시 됩니다.

  ![Windows PowerShell](./media/active-directory-report-api-with-certificates/windows-powershell.png)

### <a name="set-hello-certificate-in-your-app"></a>응용 프로그램에서 hello 인증서를 설정 합니다.
1. 앱이 이미 있는 경우 hello Azure 포털에서에서 해당 개체 ID를 가져옵니다. 

  ![Azure portal](./media/active-directory-report-api-with-certificates/azure-portal.png)

2. PowerShell 세션을 열고 tooAzure AD 연결 hello 연결-azure Ad cmdlet을 사용 합니다.

  ![Azure portal](./media/active-directory-report-api-with-certificates/connect-azuaread-cmdlet.png)

3. AzureADUtils tooadd 인증서 자격 증명 tooit에서에서 hello 새로 AzureADApplicationCertificateCredential cmdlet을 사용 합니다. 

>[!Note]
>Tooprovide hello 응용 프로그램 개체 ID는 이전에 캡처한 필요한 것은 물론 있습니다 hello 인증서 개체 (이 사용 하 여 hello Cert: 드라이브).
>


  ![Azure portal](./media/active-directory-report-api-with-certificates/add-certificate-credential.png)
  
### <a name="get-an-access-token"></a>액세스 토큰 가져오기

액세스 토큰을 tooget AzureADUtils에서 hello Get AzureADGraphAPIAccessTokenFromCert cmdlet를 사용 합니다. 

>[!NOTE]
>Hello hello 마지막 섹션에서 사용한 개체 ID 대신 toouse hello 응용 프로그램 ID가 필요 합니다.
>

 ![Azure portal](./media/active-directory-report-api-with-certificates/application-id.png)

### <a name="use-hello-access-token-toocall-hello-graph-api"></a>Hello 액세스 토큰 toocall hello Graph API를 사용 하 여

이제 hello 스크립트를 만들 수 있습니다. 다음은 hello AzureADUtils에서에서 Invoke AzureADGraphAPIQuery hello cmdlet을 사용 하는 예제입니다. 이 Cmdlet이 여러 페이지 단위 결과 처리 한 다음 해당 결과 toohello PowerShell 파이프라인을 보냅니다. 

 ![Azure portal](./media/active-directory-report-api-with-certificates/script-completed.png)

이제 CSV 준비 tooexport tooa 및 tooa SIEM 시스템을 저장 합니다. 또한에 래핑할 수 있습니다 스크립트 예약 된 작업 tooget Azure AD 데이터 테 넌 트 로부터 주기적으로 hello 소스 코드에서 toostore 응용 프로그램 키 필요 없이 합니다. 

## <a name="next-steps"></a>다음 단계
[hello Azure id 관리 기본 사항](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals-identity)<br>



