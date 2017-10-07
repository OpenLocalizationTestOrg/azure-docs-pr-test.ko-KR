---
title: "엔터프라이즈 통합 팩을 사용 하 여 aaaUsing 인증서 | Microsoft Docs"
description: "엔터프라이즈 통합 팩 hello로 toouse 인증서 하는 방법에 대해 알아봅니다 | Azure 논리 앱"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: cgronlun
ms.assetid: 4cbffd85-fe8d-4dde-aa5b-24108a7caa7d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 7ba9f597a03a852a9ba05d2af08fe4bc2d98aef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-certificates-and-enterprise-integration-pack"></a>인증서 및 엔터프라이즈 통합 팩에 대해 알아보기
## <a name="overview"></a>개요
엔터프라이즈 통합 인증서 toosecure B2B 통신을 사용합니다. 엔터프라이즈 통합 앱에서 두 가지 종류의 인증서를 사용할 수 있습니다.

* 공용 인증서는 CA(인증 기관)에서 구입해야 합니다
* 개인 인증서는 직접 발행할 수 있습니다. 이 인증서는 참조 된 tooas 자체 서명 된 인증서 때로는 합니다.

## <a name="what-are-certificates"></a>인증서란?
인증서는 전자 통신 hello 참가자의 hello id를 확인 하 고 전자 통신을 보안 하는 디지털 문서입니다.

## <a name="why-use-certificates"></a>인증서를 사용하는 이유
경우에 따라 B2B 통신을 기밀로 유지해야 합니다. 엔터프라이즈 통합 두 가지 방법으로 인증서 toosecure 이러한 통신을 사용합니다.

* 메시지의 내용을 hello를 암호화 하 여
* 메시지에 디지털로 서명하여  

## <a name="upload-a-public-certificate"></a>공용 인증서 업로드

toouse는 *공용 인증서* B2B 기능을 사용 하 여 논리 앱을 먼저 통합 계정에 tooupload hello 인증서를 필요 합니다.  

사용할 수 있는 toohelp hello에서 해당 속성을 정의 하면 B2B 메시지를 보안 인증서를 업로드 한 후에 [계약](logic-apps-enterprise-integration-agreements.md) 를 만들면 됩니다.  

Toohello Azure 포털에에서 로그인 한 후 통합 계정에 공용 인증서를 업로드 하는 자세한 단계 hello 다음과 같습니다.

1. 선택 **더 많은 서비스** 입력 **통합** hello 필터 검색 상자에 있습니다. 선택 **통합 계정** hello 결과 목록에서     
![찾아보기 선택](media/logic-apps-enterprise-integration-certificates/overview-1.png)  
2. Hello 통합 계정 toowhich tooadd hello 인증서를 선택 합니다.  
![Hello 통합 계정 toowhich tooadd hello 인증서를 선택 합니다.](media/logic-apps-enterprise-integration-certificates/overview-3.png)  
3. 선택 hello **인증서** 바둑판식으로 배열입니다.  
![선택 hello 인증서 타일](media/logic-apps-enterprise-integration-certificates/certificate-1.png)
4. Hello에 **인증서** 선택 hello 열리면 블레이드 **추가** 단추입니다.   
![Hello 추가 단추를 선택 합니다.](media/logic-apps-enterprise-integration-certificates/certificate-2.png)
5. 입력 한 **이름** 인증서 및으로 선택한 후 hello 인증서 종류에 대 한 **공용** hello 드롭다운에서 합니다.  
6. Hello의 hello 오른쪽에서 폴더 아이콘 선택 hello **인증서** 입력란. Hello 파일 선택기를 열 때 찾아 tooupload tooyour 통합 계정을 지정 하는 hello 인증서 파일을 선택 합니다.
7. Hello 인증서를 선택한 다음 선택 **확인** hello 파일 선택에서 합니다. 유효성을 검사 하 고 hello 인증서 tooyour 통합 계정에 업로드 합니다.
8. Hello에 마지막으로 백업 **인증서 추가** 블레이드, 선택 hello **확인** 단추입니다.  
![Hello 확인 단추를 선택 합니다.](media/logic-apps-enterprise-integration-certificates/certificate-3.png)  
9. 선택 hello **인증서** 바둑판식으로 배열입니다. Hello 인증서를 새로 추가 하는 것이 나타납니다.  
![Hello 새 인증서를 참조 하십시오.](media/logic-apps-enterprise-integration-certificates/certificate-4.png)  

## <a name="upload-a-private-certificate"></a>개인 인증서 업로드

toouse는 *개인 인증서* B2B 기능을 사용 하 여 논리 앱을의 개인 인증서 tooyour 통합 계정을 라인 hello 단계를 수행 하 여 업로드할 수 있습니다

1. [개인 키 tooKey 자격 증명 모음 업로드](../key-vault/key-vault-get-started.md "주요 자격 증명 모음에 알아보기") 설명과 **키 이름** 
   
   > [!TIP]
   > 주요 자격 증명 모음에서 논리 앱 tooperform 작업에 권한을 부여 해야 합니다. 다음 PowerShell 명령을 hello를 사용 하 여 액세스 toohello 논리 앱 서비스 보안 주체에 부여할 수 있습니다.`Set-AzureRmKeyVaultAccessPolicy -VaultName 'TestcertKeyVault' -ServicePrincipalName '7cd684f4-8a78-49b0-91ec-6a35d38739ba' -PermissionsToKeys decrypt, sign, get, list`  
   > 
   > 

Hello 이전 단계를 만든 후에 개인 인증서 toointegration 계정을 추가 합니다.

다음은 Azure 포털 toohello에 로그인 한 후 통합 계정에 개인 인증서를 업로드 하는 자세한 단계를 hello:  
 
1. Hello 통합 계정 toowhich hello 선택한 tooadd hello 인증서 선택 **인증서** 바둑판식으로 배열입니다.  
![선택 hello 인증서 타일](media/logic-apps-enterprise-integration-certificates/certificate-1.png)  
2. Hello에 **인증서** 선택 hello 열리면 블레이드 **추가** 단추입니다.   
![Hello 추가 단추를 선택 합니다.](media/logic-apps-enterprise-integration-certificates/certificate-2.png)
3. 입력 한 **이름** 인증서 및로 선택 hello 인증서 종류에 대 한 **개인** hello 드롭다운에서 합니다.   
4. hello hello 오른쪽에 hello 폴더 아이콘을 선택 **인증서** 입력란. Hello 파일 선택기를 열 때 원하는 tooupload tooyour 통합 계정을 hello 해당 공용 인증서를 찾습니다.   
   
   > [!Note]
   > 개인 인증서를 추가 하는 동안 반드시 tooadd 해당 공용 인증서의 tooshow [AS2 규약](logic-apps-enterprise-integration-as2.md) 수신 및 송신 설정 hello 메시지 서명 및 암호화에 대 한 합니다.
   > 
   >   

5. 선택 hello **리소스 그룹**, **주요 자격 증명 모음**, **키 이름** 및 선택 hello **확인** 단추입니다.  
![인증서 추가](media/logic-apps-enterprise-integration-certificates/privatecertificate-1.png)  
6. 선택 hello **인증서** 바둑판식으로 배열입니다. Hello 인증서를 새로 추가 하는 것이 나타납니다.
![Hello 새 인증서를 참조 하십시오.](media/logic-apps-enterprise-integration-certificates/privatecertificate-2.png)  



* [B2B 규약 만들기](logic-apps-enterprise-integration-agreements.md)  
* [Key Vault에 대해 자세히 알아보기](../key-vault/key-vault-get-started.md "주요 자격 증명 모음에 대해 알아보기")  

