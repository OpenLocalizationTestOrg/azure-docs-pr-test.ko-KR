---
title: "온-프레미스 데이터 게이트웨이 aaaInstall | Microsoft Docs"
description: "자세한 내용은 방법 tooinstall 및 온-프레미스 데이터 게이트웨이 구성 합니다."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/22/2017
ms.author: owend
ms.openlocfilehash: e2878bf765c82910d452ae2cdd9264a343ec1990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-an-on-premises-data-gateway"></a>온-프레미스 데이터 게이트웨이 설치 및 구성
온-프레미스 데이터 게이트웨이 하나 이상의 Azure Analysis Services 서버에 동일한 hello 때 필요 지역 tooon 온-프레미스 데이터 원본 연결 합니다. hello 게이트웨이에 대 한 자세한 정보는 toolearn 참조 [온-프레미스 데이터 게이트웨이](analysis-services-gateway.md)합니다.

## <a name="prerequisites"></a>필수 조건
**최소 요구 사항:**

* .NET 4.5 Framework
* 64비트 버전의 Windows 7/Windows Server 2008 R2 이상

**권장:**

* 8 코어 CPU
* 8GB 메모리
* 64비트 버전의 Windows 2012 R2 이상

**중요 고려 사항:**

* Azure와 게이트웨이 등록 하는 경우 설치를 하는 동안에 구독에 대 한 hello 기본 영역이 선택 됩니다. 다른 지역을 선택할 수 있습니다. 서버가 여러 지역에 있는 경우 각 지역에 대한 게이트웨이를 설치해야 합니다. 
* hello 게이트웨이 도메인 컨트롤러에 설치할 수 없습니다.
* 단일 컴퓨터에는 하나의 게이트웨이를 설치할 수 있습니다.
* 에 남아 있으며 toosleep는 설명 하지 않습니다 하는 컴퓨터에서 hello 게이트웨이 설치 합니다.
* 컴퓨터 tooyour 무선으로 연결 된 네트워크의 hello 게이트웨이 설치 하지 마십시오. 성능이 감소될 수 있습니다.


## <a name="download"></a>다운로드
 [Hello 게이트웨이 다운로드 합니다.](https://aka.ms/azureasgateway)

## <a name="install"></a>설치

1. 설치를 실행합니다.

2. 위치 선택, hello 조건에 동의 하 고 클릭 **설치**합니다.

   ![설치 위치 및 사용 조건](media/analysis-services-gateway-install/aas-gateway-installer-accept.png)

3. **온-프레미스 데이터 게이트웨이(권장)**를 선택합니다. Azure Analysis Services는 개인 모드를 지원하지 않습니다.

   ![게이트웨이 유형 선택](media/analysis-services-gateway-install/aas-gateway-installer-shared.png)

4. 계정 toosign tooAzure 입력 합니다. hello 계정은 테 넌 트의 Azure Active Directory에 있어야 합니다. 이 계정은 hello 게이트웨이 관리자에 사용 됩니다. 

   ![계정 toosign tooAzure에 입력](media/analysis-services-gateway-install/aas-gateway-installer-account.png)

   > [!NOTE]
   > 도메인 계정으로 로그인 하는 경우 tooyour 조직 계정을 Azure AD에 매핑됩니다. 조직 계정으로 hello 게이트웨이 관리자에 게 사용 됩니다.

## <a name="register"></a>등록
순서 toocreate Azure에서 게이트웨이 리소스 hello 게이트웨이 클라우드 서비스와 함께 설치 하는 hello 로컬 인스턴스를 등록 해야 합니다. 

1.  **이 컴퓨터에 새 게이트웨이 등록**을 선택합니다.

    ![등록](media/analysis-services-gateway-install/aas-gateway-register-new.png)

2. 게이트웨이에 대한 이름 및 복구 키를 입력합니다. 기본적으로 hello 게이트웨이 구독의 기본 영역을 사용합니다. 다른 지역 tooselect 필요한 경우에 선택 **변경 지역**합니다.

   ![등록](media/analysis-services-gateway-install/aas-gateway-register-name.png)


## <a name="create-resource"></a>Azure 게이트웨이 리소스 만들기
설치 된 게이트웨이 등록 한 후 Azure 구독에서 게이트웨이 리소스 toocreate가 필요 합니다. Hello로 tooAzure에 동일한 로그인 hello 게이트웨이 등록할 때 사용 되는 계정입니다.

1. Azure Portal에서 **새 서비스 만들기** > **엔터프라이즈 통합** > **온-프레미스 데이터 게이트웨이** > **만들기**를 클릭합니다.

   ![게이트웨이 리소스 만들기](media/analysis-services-gateway-install/aas-gateway-new-azure-resource.png)

2. **연결 게이트웨이 만들기**에서 이러한 설정을 입력합니다.

    * **이름**: 게이트웨이 리소스의 이름을 입력합니다. 

    * **구독**: 선택 hello 게이트웨이 리소스와 Azure 구독 tooassociate 합니다. 
    이 구독 해야 hello 서버에 있는 동일한 구독 합니다.
   
      hello 기본 구독 hello toosign에 사용한 Azure 계정 기반으로 합니다.

    * **리소스 그룹**: 리소스 그룹을 만들거나 기존 리소스 그룹을 선택합니다.

    * **위치**: hello 선택 영역에 게이트웨이 등록 합니다.

    * **설치 이름**: 게이트웨이 설치 선택 되어 있지 않으면 선택 hello 게이트웨이 등록 합니다. 

    완료하면 **만들기**를 클릭합니다.

## <a name="connect-servers"></a>서버 toohello 게이트웨이 리소스를 연결 합니다.

1. Azure Analysis Services 서버 개요에서 **온-프레미스 데이터 게이트웨이**를 클릭합니다.

   ![서버 toogateway 연결](media/analysis-services-gateway-install/aas-gateway-connect-server.png)

2. **온-프레미스 데이터 게이트웨이 tooconnect 선택**게이트웨이 리소스를 선택한 다음 클릭 **연결 선택한 게이트웨이**합니다.

   ![서버 toogateway 리소스 연결](media/analysis-services-gateway-install/aas-gateway-connect-resource.png)

    > [!NOTE]
    > 게이트웨이 hello 목록에 나타나지 않으면 서버 가능성이 없는 경우에 hello hello 게이트웨이 등록 하는 경우 지정한 hello 영역으로 같은 지역입니다. 

이것으로 끝입니다. 모든 문제 해결을 수행 하거나 tooopen 포트를 필요한 경우 수 있는지 toocheck 아웃 [온-프레미스 데이터 게이트웨이](analysis-services-gateway.md)합니다.

## <a name="next-steps"></a>다음 단계
* [Analysis Services 관리](analysis-services-manage.md)   
* [Azure Analysis Services에서 데이터 가져오기](analysis-services-connect.md)
