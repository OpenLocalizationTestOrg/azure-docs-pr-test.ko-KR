---
title: "Azure CLI 스크립트 - PostgreSQL용 Azure Database 만들기 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - PostgreSQL 서버용 Azure Database를 만들고 서버 수준 방화벽 규칙을 구성합니다."
services: postgresql
author: salonisonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: azure-cli
ms.topic: sample
ms.date: 05/31/2017
ms.openlocfilehash: e545b568cd57fdcf28ab33a5ebfa34a495111c7f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-azure-database-for-postgresql-server-and-configure-a-firewall-rule-using-the-azure-cli"></a><span data-ttu-id="0e0f4-103">Azure CLI를 사용하여 PostgreSQL 서버용 Azure Database 만들기 및 방화벽 규칙 구성</span><span class="sxs-lookup"><span data-stu-id="0e0f4-103">Create an Azure Database for PostgreSQL server and configure a firewall rule using the Azure CLI</span></span>
<span data-ttu-id="0e0f4-104">이 샘플 CLI 스크립트는 PostgreSQL 서버용 Azure Database를 만들고 서버 수준 방화벽 규칙을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0f4-104">This sample CLI script creates an Azure Database for PostgreSQL server and configures a server-level firewall rule.</span></span> <span data-ttu-id="0e0f4-105">스크립트가 성공적으로 실행되면 모든 Azure 서비스 및 구성된 IP 주소에서 PostgreSQL 서버에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e0f4-105">Once the script has been successfully run, the PostgreSQL server can be accessed from all Azure services and the configured IP address.</span></span>

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="0e0f4-106">CLI를 로컬로 설치하여 사용하도록 선택한 경우 이 항목에서 Azure CLI 버전 2.0 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0f4-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="0e0f4-107">`az --version`을 실행하여 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="0e0f4-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="0e0f4-108">설치 또는 업그레이드해야 하는 경우 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0e0f4-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="0e0f4-109">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="0e0f4-109">Sample script</span></span>
<span data-ttu-id="0e0f4-110">이 샘플 스크립트에서 강조 표시된 줄을 편집하여 관리자 사용자 이름 및 암호를 사용자 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0f4-110">In this sample script, edit the highlighted lines to customize the admin username and password.</span></span>
<span data-ttu-id="0e0f4-111">[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/create-postgresql-server-and-firewall-rule.sh?highlight=15-16 "PostgreSQL용 Azure 데이터베이스 및 서버 수준 방화벽 규칙을 만듭니다.")]</span><span class="sxs-lookup"><span data-stu-id="0e0f4-111">[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/create-postgresql-server-and-firewall-rule.sh?highlight=15-16 "Create an Azure Database for PostgreSQL, and server-level firewall rule.")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="0e0f4-112">배포 정리</span><span class="sxs-lookup"><span data-stu-id="0e0f4-112">Clean up deployment</span></span>
<span data-ttu-id="0e0f4-113">스크립트 샘플을 실행한 후에 다음 명령을 사용하여 리소스 그룹 및 관련된 모든 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e0f4-113">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>
<span data-ttu-id="0e0f4-114">[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/delete-postgresql.sh "리소스 그룹을 삭제합니다.")]</span><span class="sxs-lookup"><span data-stu-id="0e0f4-114">[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/delete-postgresql.sh "Delete the resource group.")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="0e0f4-115">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="0e0f4-115">Script explanation</span></span>
<span data-ttu-id="0e0f4-116">이 스크립트는 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0f4-116">This script uses the following commands.</span></span> <span data-ttu-id="0e0f4-117">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e0f4-117">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="0e0f4-118">**명령**</span><span class="sxs-lookup"><span data-stu-id="0e0f4-118">**Command**</span></span> | <span data-ttu-id="0e0f4-119">**참고 사항**</span><span class="sxs-lookup"><span data-stu-id="0e0f4-119">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="0e0f4-120">az group create</span><span class="sxs-lookup"><span data-stu-id="0e0f4-120">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="0e0f4-121">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0e0f4-121">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="0e0f4-122">az postgres server create</span><span class="sxs-lookup"><span data-stu-id="0e0f4-122">az postgres server create</span></span>](/cli/azure/postgres/server#create) | <span data-ttu-id="0e0f4-123">데이터베이스를 호스팅하는 PostgreSQL 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0e0f4-123">Creates a PostgreSQL server that hosts the databases.</span></span> |
| [<span data-ttu-id="0e0f4-124">az postgres server firewall create</span><span class="sxs-lookup"><span data-stu-id="0e0f4-124">az postgres server firewall create</span></span>](/cli/azure/postgres/server/firewall-rule#create) | <span data-ttu-id="0e0f4-125">입력한 IP 주소 범위의 서버에서 서버 및 서버의 데이터베이스에 액세스할 수 있도록 방화벽 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0e0f4-125">Creates a firewall rule to allow access to the server and databases under it from the entered IP address range.</span></span> |
| [<span data-ttu-id="0e0f4-126">az group delete</span><span class="sxs-lookup"><span data-stu-id="0e0f4-126">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="0e0f4-127">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0f4-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0e0f4-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0e0f4-128">Next steps</span></span>
- <span data-ttu-id="0e0f4-129">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0e0f4-129">Read more information on the Azure CLI: [Azure CLI documentation](/cli/azure/overview)</span></span>
- <span data-ttu-id="0e0f4-130">추가 스크립트 시도: [PostgreSQL용 Azure 데이터베이스 대한 Azure CLI 샘플](../sample-scripts-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="0e0f4-130">Try additional scripts: [Azure CLI samples for Azure Database for PostgreSQL](../sample-scripts-azure-cli.md)</span></span>
