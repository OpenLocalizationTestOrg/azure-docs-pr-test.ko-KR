---
title: "aaaTroubleshoot Azure 가상 네트워크 게이트웨이 및 연결-Azure CLI 1.0 | Microsoft Docs"
description: "이 페이지에서는 Azure 네트워크 감시자 toouse hello Azure CLI 1.0을 해결 하는 방법을 설명 합니다."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2838bc61-b182-4da8-8533-27db8fdbd177
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: a0511689d773f9c7216b0fe5470e27f754eb600b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-azure-cli-10"></a>Azure Network Watcher Azure CLI 1.0을 사용하여 Virtual Network 게이트웨이 및 연결 문제 해결

> [!div class="op_single_selector"]
> - [포털](network-watcher-troubleshoot-manage-portal.md)
> - [PowerShell](network-watcher-troubleshoot-manage-powershell.md)
> - [CLI 1.0](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [CLI 2.0](network-watcher-troubleshoot-manage-cli.md)
> - [REST API](network-watcher-troubleshoot-manage-rest.md)

네트워크 감시자 toounderstanding Azure의 네트워크 리소스 관련해 서 다양 한 기능을 제공 합니다. 이러한 기능 중 하나는 리소스 문제 해결입니다. 리소스 문제를 해결 하는 hello 포털, PowerShell, CLI 또는 REST API를 통해 호출할 수 있습니다. 호출 되 면 네트워크 감시자 가상 네트워크 게이트웨이 또는 연결의 hello 상태를 검사 하 고 해당 결과 반환 합니다.

이 문서에서는 Windows, Mac 및 Linux에 사용할 수 있는 플랫폼 간 Azure CLI 1.0을 사용합니다. 

## <a name="before-you-begin"></a>시작하기 전에

이 시나리오에서는 hello 단계에 따라 이미 가정 [네트워크 감시자를 만들](network-watcher-create.md) toocreate 네트워크 감시자 합니다.

지원되는 게이트웨이 유형 목록을 보려면 [지원되는 게이트웨이 유형](/network-watcher-troubleshoot-overview.md#supported-gateway-types)을 방문하세요.

## <a name="overview"></a>개요

Hello 기능을 제공 리소스 문제 해결 가상 네트워크 게이트웨이 및 연결 때 발생 하는 문제를 해결 합니다. 요청이 이루어지면 tooresource 문제 해결 로그 되는 쿼리 및 검사 합니다. 검사 완료 되 면 hello 결과가 반환 됩니다. 결과 여러 분 tooreturn를 수행할 수 있는 리소스 문제 해결 요청은 장기 실행 요청 합니다. 문제 해결에서 hello 로그에 지정 된 저장소 계정에 대 한 컨테이너에 저장 됩니다.

## <a name="retrieve-a-virtual-network-gateway-connection"></a>Virtual Network 게이트웨이 연결 검색

이 예제에서 리소스 문제 해결은 연결에서 실행됩니다. Virtual Network 게이트웨이를 전달할 수도 있습니다. hello 다음 cmdlet 나열 hello vpn-리소스 그룹에 연결 합니다.

```azurecli
azure network vpn-connection list -g resourceGroupName
```

작업을 구독에 hello 연결 hello 명령 toosee로 실행할 수도 있습니다.

```azurecli
azure network vpn-connection list -s subscription
```

Hello 연결의 이름을 hello를 만든 후 해당 리소스 Id에이 명령은 tooget 실행할 수 있습니다.

```azurecli
azure network vpn-connection show -g resourceGroupName -n connectionName
```

## <a name="create-a-storage-account"></a>저장소 계정 만들기

Hello 리소스의 hello 상태에 대 한 데이터를 반환 리소스 문제 해결, 로그 tooa 저장소 계정 toobe 검토를 저장 합니다. 이 단계에서는 저장소 계정을 만듭니다. 기존 저장소 계정이 있는 경우 사용할 수 있습니다.

1. Hello 저장소 계정 만들기

    ```azurecli
    azure storage account create -n storageAccountName -l location -g resourceGroupName
    ```

1. Hello 저장소 계정 키 가져오기

    ```azurecli
    azure storage account keys list storageAccountName -g resourcegroupName
    ```

1. Hello 컨테이너 만들기

    ```azurecli
    azure storage container create --account-name storageAccountName -g resourcegroupName --account-key {storageAccountKey} --container logs
    ```

## <a name="run-network-watcher-resource-troubleshooting"></a>Network Watcher 리소스 문제 해결 실행

Hello 사용 하 여 리소스 문제를 해결 `network watcher troubleshoot` cmdlet. Hello cmdlet hello 리소스 그룹 전달 하 고 hello hello 네트워크 감시자를 hello hello 연결의 Id의 이름 hello hello 저장소 계정의 Id hello 경로 toohello blob toostore hello 문제에서 결과 해결 합니다.

```azurecli
azure network watcher troubleshoot -g resourceGroupName -n networkWatcherName -t connectionId -i storageId -p storagePath
```

Hello cmdlet을 실행 한 후 네트워크 감시자 hello 리소스 tooverify hello 상태를 검토 합니다. Toohello 셸 hello 결과 반환 합니다. 지정 된 hello 저장소 계정에 hello 결과의 로그를 보관 합니다.

## <a name="understanding-hello-results"></a>Hello 결과 이해

hello 동작 텍스트 tooresolve 문제 hello 하는 방법에 대 한 일반적인 지침을 제공 합니다. Hello 문제에 대 한 작업을 수행할 수, 링크를 추가 하는 지침과 함께 제공 됩니다. Hello 경우에서 hello 응답을 자세한 지침은 없으며가 있는 hello url tooopen 지원 사례를 제공 합니다.  Hello 응답 및 포함 된 항목의 hello 속성에 대 한 자세한 내용은 방문 [네트워크 감시자 문제 해결 개요](network-watcher-troubleshoot-overview.md)

Azure 저장소 계정에서 파일을 다운로드 하는 방법은 참조 너무[.NET을 사용 하 여 Azure Blob 저장소 시작](../storage/blobs/storage-dotnet-how-to-use-blobs.md)합니다. 사용할 수 있는 다른 도구는 저장소 탐색기입니다. 저장소 탐색기에 대 한 자세한 내용은 여기에 있습니다 링크 hello: [저장소 탐색기](http://storageexplorer.com/)

## <a name="next-steps"></a>다음 단계

해당 중지 VPN 연결 설정이 변경 되었으며, 참조 [네트워크 보안 그룹 관리](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack 아래로 hello 네트워크 보안 그룹 및 보안 규칙을 문제가 될 수 있습니다.
