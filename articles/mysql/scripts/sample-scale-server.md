---
title: "MySQL 서버용 Azure Database를 확장하는 Azure CLI 샘플 | Microsoft Docs"
description: "이 샘플 CLI 스크립트는 메트릭을 쿼리한 후에 MySQL 서버용 Azure Database를 다양한 성능 수준으로 확장합니다."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: sample
ms.custom: mvc
ms.date: 05/31/2017
ms.openlocfilehash: 33316ff3db382d25a444d55772c6ee4d7b7ac418
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-and-scale-an-azure-database-for-mysql-server-using-azure-cli"></a><span data-ttu-id="bc0be-103">Azure CLI를 사용하여 MySQL용 Azure Database 모니터링 및 확장</span><span class="sxs-lookup"><span data-stu-id="bc0be-103">Monitor and scale an Azure Database for MySQL server using Azure CLI</span></span>
<span data-ttu-id="bc0be-104">이 샘플 CLI 스크립트는 메트릭을 쿼리한 후에 MySQL 서버용 단일 Azure Database를 다양한 성능 수준으로 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="bc0be-104">This sample CLI script scales a single Azure Database for MySQL server to a different performance level after querying the metrics.</span></span>

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="bc0be-105">CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 항목에서 Azure CLI 버전 2.0 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc0be-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="bc0be-106">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="bc0be-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="bc0be-107">설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bc0be-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="bc0be-108">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="bc0be-108">Sample script</span></span>
<span data-ttu-id="bc0be-109">이 샘플 스크립트에서 강조 표시된 줄을 변경하여 관리자 사용자 이름 및 암호를 사용자 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bc0be-109">In this sample script, change the highlighted lines to customize the admin username and password.</span></span> <span data-ttu-id="bc0be-110">az monitor 명령에 사용된 구독 ID를 사용자 고유의 구독 ID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="bc0be-110">Replace the subscription id used in the az monitor commands with your own subscription id.</span></span>
<span data-ttu-id="bc0be-111">[!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/scale-mysql-server.sh?highlight=15-16 "MySQL용 Azure 데이터베이스를 만들고 크기를 조정합니다.")]</span><span class="sxs-lookup"><span data-stu-id="bc0be-111">[!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/scale-mysql-server.sh?highlight=15-16 "Create and scale Azure Database for MySQL.")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="bc0be-112">배포 정리</span><span class="sxs-lookup"><span data-stu-id="bc0be-112">Clean up deployment</span></span>
<span data-ttu-id="bc0be-113">스크립트 샘플을 실행한 후에 다음 명령을 사용하여 리소스 그룹 및 관련된 모든 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc0be-113">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>
<span data-ttu-id="bc0be-114">[!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/delete-mysql.sh  "리소스 그룹을 삭제합니다.")]</span><span class="sxs-lookup"><span data-stu-id="bc0be-114">[!code-azurecli-interactive[main](../../../cli_scripts/mysql/scale-mysql-server/delete-mysql.sh  "Delete the resource group.")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="bc0be-115">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="bc0be-115">Script explanation</span></span>
<span data-ttu-id="bc0be-116">이 스크립트는 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bc0be-116">This script uses the following commands.</span></span> <span data-ttu-id="bc0be-117">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc0be-117">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="bc0be-118">**명령**</span><span class="sxs-lookup"><span data-stu-id="bc0be-118">**Command**</span></span> | <span data-ttu-id="bc0be-119">**참고 사항**</span><span class="sxs-lookup"><span data-stu-id="bc0be-119">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="bc0be-120">az group create</span><span class="sxs-lookup"><span data-stu-id="bc0be-120">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="bc0be-121">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bc0be-121">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="bc0be-122">az mysql server create</span><span class="sxs-lookup"><span data-stu-id="bc0be-122">az mysql server create</span></span>](/cli/azure/mysql/server#create) | <span data-ttu-id="bc0be-123">데이터베이스를 호스팅하는 MySQL 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bc0be-123">Creates a MySQL server that hosts the databases.</span></span> |
| [<span data-ttu-id="bc0be-124">az monitor metrics list</span><span class="sxs-lookup"><span data-stu-id="bc0be-124">az monitor metrics list</span></span>](/cli/azure/monitor/metrics#list) | <span data-ttu-id="bc0be-125">리소스에 대한 메트릭 값을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="bc0be-125">List the metric value for the resources.</span></span> |
| [<span data-ttu-id="bc0be-126">az group delete</span><span class="sxs-lookup"><span data-stu-id="bc0be-126">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="bc0be-127">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="bc0be-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="bc0be-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bc0be-128">Next steps</span></span>
- <span data-ttu-id="bc0be-129">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bc0be-129">Read more information on the Azure CLI: [Azure CLI documentation](/cli/azure/overview).</span></span>
- <span data-ttu-id="bc0be-130">추가 스크립트 시도: [MySQL용 Azure 데이터베이스 대한 Azure CLI 샘플](../sample-scripts-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="bc0be-130">Try additional scripts: [Azure CLI samples for Azure Database for MySQL](../sample-scripts-azure-cli.md)</span></span>
- <span data-ttu-id="bc0be-131">확장에 대한 자세한 내용은 [서비스 계층](../concepts-service-tiers.md) 및 [계산 단위 및 저장 단위](../concepts-compute-unit-and-storage.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bc0be-131">For more information on scaling, see [Service Tiers](../concepts-service-tiers.md) and [Compute Units and Storage Units](../concepts-compute-unit-and-storage.md).</span></span>
