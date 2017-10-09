---
title: "aaaAzure CLI 스크립트 샘플-일괄 처리 계정 만들기 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - 배치 계정 만들기"
services: batch
documentationcenter: 
author: annatisch
manager: daryls
editor: tysonn
ms.assetid: 
ms.service: batch
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/02/2017
ms.author: antisch
ms.openlocfilehash: 62b640eebbafdd1081822a638fd0720121ef067a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-batch-account-with-hello-azure-cli"></a>Hello Azure CLI로 일괄 처리 계정 만들기

이 스크립트는 Azure 배치 계정을 만들고 고 hello 계정의 다양 한 속성을 쿼리할 업데이트 하 고 보여 줍니다.

## <a name="prerequisites"></a>필수 조건

설치 hello hello에 제공 된 hello 지침을 사용 하 여 Azure CLI [Azure CLI 설치 가이드](https://docs.microsoft.com/cli/azure/install-azure-cli)아직 수행 하지 않은 경우.

## <a name="batch-account-sample-script"></a>배치 계정 샘플 스크립트

일괄 처리 계정을 만들 때 기본적으로는 계산 노드 할당 내부적으로 hello 일괄 처리 서비스 합니다. 할당 된 계산 노드 제목 tooa 별도 코어 할당량 되며 hello 계정 공유 키 자격 증명 또는 Azure Active Dirctory 토큰을 통해 인증할 수 있습니다.

[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account.sh "Create Account")]

## <a name="batch-account-using-user-subscription-sample-script"></a>사용자 구독을 사용하는 배치 계정 샘플 스크립트

선택할 수 있습니다 일괄 처리 toohave Azure 구독에서의 계산 노드 만들기.
계정을 할당 하는 노드를 구독으로 Azure Active Directory 토큰을 통해 인증 되어야 하며 현재 구독 할당량이 진행할 할당 된 hello 계산 노드 수를 계산 합니다. 이 모드에서는 계정 toocreate hello 계정을 만들 때 자격 증명 모음 키 참조를 지정 해야 하나 합니다.

[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account-user-subscription.sh  "Create Account using User Subscription")]

## <a name="clean-up-deployment"></a>배포 정리

Hello 위의 예제 스크립트를 실행 한 후 리소스 그룹과 관련 된 모든 리소스 (일괄 처리 계정, Azure 저장소 계정 및 Azure 키 자격 증명 모음은 포함) hello 명령 tooremove 다음을 실행 합니다.

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>스크립트 설명

이 스크립트 명령 toocreate 리소스 그룹, 일괄 처리 계정 및 모든 관련된 리소스를 수행 하는 hello를 사용 합니다. Hello 테이블 링크 toocommand 특정 설명서에서 각 명령입니다.

| 명령 | 참고 사항 |
|---|---|
| [az group create](https://docs.microsoft.com/cli/azure/group#create) | 모든 리소스가 저장되는 리소스 그룹을 만듭니다. |
| [az batch account create](https://docs.microsoft.com/cli/azure/batch/account#create) | Hello 일괄 처리 계정을 만듭니다.  |
| [az batch account set](https://docs.microsoft.com/cli/azure/batch/account#set) | 일괄 처리 계정 hello의 속성을 업데이트 합니다.  |
| [az batch account show](https://docs.microsoft.com/cli/azure/batch/account#show) | 일괄 처리 계정을 지정 하는 hello의 검색 세부 정보.  |
| [az batch account keys list](https://docs.microsoft.com/cli/azure/batch/account/keys#list) | 일괄 처리 계정을 지정 하는 hello의 hello 선택 키를 검색 합니다.  |
| [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login) | 지정 된 hello에 대 한 인증 계정을 더 이상의 CLI 상호 작용에 대 한 일괄 처리 합니다.  |
| [az storage account create](https://docs.microsoft.com/cli/azure/storage/account#create) | 저장소 계정을 만듭니다. |
| [az keyvault create](https://docs.microsoft.com/cli/azure/keyvault#create) | 키 자격 증명 모음을 만듭니다. |
| [az keyvault set-policy](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | Hello 지정 된 키 자격 증명 모음의 hello 보안 정책을 업데이트 합니다. |
| [az group delete](https://docs.microsoft.com/cli/azure/group#delete) | 모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다. |

## <a name="next-steps"></a>다음 단계

Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.

추가 일괄 처리 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure 일괄 처리 CLI 설명서](../batch-cli-samples.md)합니다.
