---
title: "CLI 2.0 aaaUse toocreate Azure AD 앱 및 tooaccess Azure 미디어 서비스 API 구성 | Microsoft Docs"
description: "이 항목에서는 방법을 toouse CLI 2.0 toocreate Azure AD 앱 및 tooaccess Azure 미디어 서비스 API를 구성 합니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: c865e2701722374b5dd17b0e20fa848c07065006
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-20-toocreate-an-aad-app-and-configure-it-tooaccess-azure-media-services-api"></a>CLI 2.0 toocreate AAD 응용 프로그램을 사용 하 고 Azure 미디어 서비스 API tooaccess 구성

이 항목에서는 방법을 toouse CLI 2.0 toocreate Azure Active Directory (Azure AD) 응용 프로그램 및 서비스 보안 주체 tooaccess Azure 미디어 서비스 리소스입니다. 

## <a name="prerequisites"></a>필수 조건

- Azure 계정. 자세한 내용은 [Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요. 
- Media Services 계정. 자세한 내용은 참조 [hello Azure 포털을 사용 하 여 Azure 미디어 서비스 계정 만들기](media-services-portal-create-account.md)합니다.

## <a name="use-hello-azure-cloud-shell"></a>Azure 클라우드 셸 hello를 사용 하 여

1. Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.
2. Hello 클라우드 셸 hello 포털의 hello 위쪽 탐색 창에서 시작 합니다.

    ![Cloud Shell](./media/media-services-cli-create-and-configure-aad-app/media-services-cli-create-and-configure-aad-app01.png) 

자세한 내용은 [Azure Cloud Shell 개요](../cloud-shell/overview.md)를 참조하세요.

## <a name="create-an-azure-ad-app-and-configure-access-toohello-media-account-with-cli-20"></a>Azure AD 앱을 만들고 액세스 toohello 미디어 계정을 CLI 2.0 구성
 
```azurecli
az login
az ad sp create-for-rbac --name <appName> --password <strong password>
az role assignment create -- assignee < user/app id> --role Contributor --scope <subscription/subscription id>
```

예:

```azurecli
az role assignment create --assignee a3e068fa-f739-44e5-ba4d-ad57866e25a1 --role Contributor --scope /subscriptions/0b65e280-7917-4874-9fed-1307f2615ea2/resourceGroups/Default-AzureBatch-SouthCentralUS/providers/microsoft.media/mediaservices/sbbash
```

이 예제에서는 hello **범위** hello 전체 리소스 경로 hello 미디어에 대 한 서비스 계정입니다. 그러나 hello **범위** 모든 수준에 있을 수 있습니다.

예를 들어 hello 수준을 다음 중 하나 수 있습니다.
 
* hello **구독** 수준입니다.
* hello **리소스 그룹** 수준입니다.
* hello **리소스** 수준 (예를 들어 미디어 계정).

자세한 내용은 [Azure CLI 2.0을 사용하여 Azure 서비스 주체 만들기](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli)를 참조하세요.

또한 참조 [hello Azure 명령줄 인터페이스와 Manage Role-Based 액세스 제어](../active-directory/role-based-access-control-manage-access-azure-cli.md)합니다. 

## <a name="next-steps"></a>다음 단계

시작 [tooyour 계정에 파일 업로드](media-services-portal-upload-files.md)합니다.
