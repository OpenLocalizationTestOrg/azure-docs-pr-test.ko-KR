---
title: "Azure 관리 API 인증서 aaaUpload | Microsoft Docs"
description: "관리 API tooupload 사용자별 hello Azure 클래식 포털에 대 한 인증서는 방법에 대해 알아봅니다."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 1b813833-39c8-46be-8666-fd0960cfbf04
ms.service: na
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: adegeo
ms.openlocfilehash: 8294d7131cfb01dba664bd4fd04b6fc22c1e93ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-an-azure-management-api-management-certificate"></a>Azure 관리 API Management 인증서 업로드
관리 인증서를 사용 하면 tooauthenticate hello 클래식 배포 모델에는 Azure에서 제공 합니다. 많은 프로그램 및 도구 (예: Visual Studio 또는 Azure SDK hello) 이러한 인증서 tooautomate 구성 및 다양 한 Azure 서비스의 배포를 사용 합니다. 

> [!WARNING]
> 주의가 필요합니다! 모든 사용자가 사용 하 여 인증을 허용 하는 이러한 종류의 인증서는 연결 된 toomanage hello 구독 합니다.
>
>

Azure 인증서(자체 서명 인증서 포함)에 대한 자세한 내용은 [Azure Cloud Services에 대한 인증서 개요](cloud-services/cloud-services-certs-create.md#what-are-management-certificates)를 참조하세요.

사용할 수도 있습니다 [Azure Active Directory](https://azure.microsoft.com/en-us/services/active-directory/) 자동화 목적을 위해 tooauthenticate 클라이언트 코드입니다.

## <a name="upload-a-management-certificate"></a>관리 인증서 업로드
만든 관리 인증서, (hello 공개 키만.cer 파일)를 수행한 hello 포털에 업로드할 수 있습니다. Hello 인증서 hello 포털에 표시 되 면 일치 하는 인증서 (개인 키 포함)를 가진 사람이 면 누구나 hello 연결 된 구독에 대 한 hello 관리 API 및 액세스 hello 리소스를 통해 연결할 수 있습니다.

1. Toohello 로그인 [Azure 포털](http://portal.azure.com)합니다.
2. 클릭 **더 많은 서비스** hello 아래 Azure 서비스 목록에서 선택 **구독** hello에 _일반_ 서비스 그룹입니다.

    ![구독 메뉴](./media/azure-api-management-certs/subscriptions_menu.png)

3. Tooselect hello tooassociate hello 인증서로 지정 하는 올바른 구독이 있는지 확인 합니다.     
4. Hello 올바른 구독을 선택한 후 키를 눌러 **관리 인증서** hello에 _설정을_ 그룹입니다.

    ![설정](./media/azure-api-management-certs/mgmtcerts_menu.png)

5. 키를 눌러 hello **업로드** 단추입니다.

    ![인증서 페이지에 업로드](./media/azure-api-management-certs/certificates_page.png)
6. Hello 대화 정보 및 키를 눌러 입력 **업로드**합니다.

    ![설정](./media/azure-api-management-certs/certificate_details.png)

## <a name="next-steps"></a>다음 단계
구독에 연결 된 관리 인증서를가지고 연결할 수 있습니다 (설치한 경우 로컬로 인증서와 일치 하는 hello) 프로그래밍 방식으로 toohello [클래식 배포 모델 REST API](https://msdn.microsoft.com/library/azure/mt420159.aspx) 및 자동화 안녕 다양 한 Azure 리소스도 해당 구독과 연결 됩니다.
