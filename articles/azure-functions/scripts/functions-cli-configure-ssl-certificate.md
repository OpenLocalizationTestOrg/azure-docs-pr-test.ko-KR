---
title: "aaaAzure CLI 스크립트 샘플-바인딩 사용자 지정 SSL 인증서 tooa 함수 앱 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플-Azure에는 사용자 지정 SSL 인증서 tooa 함수 앱 바인딩"
services: functions
documentationcenter: 
author: ggailey777
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: eb95d350-81ea-4145-a1e2-6eea3b7469b2
ms.service: functions
ms.workload: na
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 04/10/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 692dbc03583f2978131823083f1bfd257882664c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="bind-a-custom-ssl-certificate-tooa-function-app"></a>사용자 지정 SSL 인증서 tooa 함수 앱 바인딩

이 샘플 스크립트과 해당 관련된 리소스 응용 프로그램 서비스에서 함수 응용 프로그램을 만듭니다 다음 사용자 지정 도메인 이름 tooit의 hello SSL 인증서를 바인딩합니다. 이 샘플에는 다음이 필요합니다.

* Tooyour 도메인 등록자의 DNS 구성 페이지에 액세스 합니다.
* 유효 합니다. PFX 파일 및 SSL hello에 대 한 암호 인증서 tooupload 원하고 바인딩합니다.

SSL 인증서 toobind 소비 계획 아니라 앱 서비스 계획에 함수 앱을 만들 수 해야 합니다.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Tooinstall를 선택 하 고 로컬로 hello CLI를 사용 하 여이 항목 2.0 이상에 hello Azure CLI 버전을 실행 중인 필요 합니다. 실행 `az --version` toofind hello 버전입니다. Tooinstall 또는 업그레이드를 보려면 참고 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)합니다. 

## <a name="sample-script"></a>샘플 스크립트

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate tooa web app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>스크립트 설명

이 스크립트 명령 뒤 hello를 사용 합니다. Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.

| 명령 | 참고 사항 |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | 모든 리소스가 저장되는 리소스 그룹을 만듭니다. |
| [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) | 앱 서비스 계획이 필요 toobind SSL 인증서를 만듭니다. |
| [az functionapp create]() | 함수 앱을 만듭니다. |
| [az appservice web config hostname add](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | 사용자 지정 도메인 toohello 함수 응용 프로그램을 매핑합니다. |
| [az appservice web config ssl upload](https://docs.microsoft.com/cli/azure/appservice/web/config/ssl#upload) | SSL 인증서 tooa 함수 앱을 업로드합니다. |
| [az appservice web config ssl bind](https://docs.microsoft.com/en-us/cli/azure/appservice/web/config/ssl#bind) | 업로드 된 SSL 인증서 tooa 함수 앱에 바인딩합니다. |

## <a name="next-steps"></a>다음 단계

Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.

추가 응용 프로그램 서비스 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure 앱 서비스 설명서]()합니다.
