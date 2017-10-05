---
title: "Azure Data Factory를 사용하여 온-프레미스 SQL Server에서 SQL Azure로 데이터 이동 | Microsoft Docs"
description: "온-프레미스와 클라우드의 데이터베이스 간에 데이터를 매일 이동하는 두 데이터 마이그레이션 활동으로 구성된 ADF 파이프라인을 설정합니다."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 36837c83-2015-48be-b850-c4346aa5ae8a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 39fe26d3388be8b558f05063a8965889c013a41e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-from-an-on-premises-sql-server-to-sql-azure-with-azure-data-factory"></a><span data-ttu-id="e5aea-103">Azure Data Factory를 사용하여 온-프레미스 SQL Server에서 SQL Azure로 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="e5aea-103">Move data from an on-premises SQL server to SQL Azure with Azure Data Factory</span></span>
<span data-ttu-id="e5aea-104">이 토픽에서는 ADF(Azure Data Factory)를 사용하여 Azure Blob Storage를 통해 온-프레미스 SQL Server Database에서 SQL Azure Database로 데이터를 이동하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-104">This topic shows how to move data from an on-premises SQL Server Database to a SQL Azure Database via Azure Blob Storage using the Azure Data Factory (ADF).</span></span>

<span data-ttu-id="e5aea-105">Azure SQL Database로 데이터를 이동하는 다양한 옵션을 요약한 표는 [Azure Machine Learning을 위해 Azure SQL Database로 데이터 이동](machine-learning-data-science-move-sql-azure.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e5aea-105">For a table that summarizes various options for moving data to an Azure SQL Database, see [Move data to an Azure SQL Database for Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).</span></span>

## <span data-ttu-id="e5aea-106"><a name="intro"></a>소개: ADF란 무엇이며 데이터를 마이그레이션하는 데 사용하려면 언제 사용해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="e5aea-106"><a name="intro"></a>Introduction: What is ADF and when should it be used to migrate data?</span></span>
<span data-ttu-id="e5aea-107">Azure 데이터 팩터리는 데이터의 이동과 변환을 오케스트레이션하고 자동화하는 완전히 관리되는 클라우드 기반의 데이터 통합 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-107">Azure Data Factory is a fully managed cloud-based data integration service that orchestrates and automates the movement and transformation of data.</span></span> <span data-ttu-id="e5aea-108">ADF 모델의 핵심 개념은 파이프라인입니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-108">The key concept in the ADF model is pipeline.</span></span> <span data-ttu-id="e5aea-109">파이프라인은 각각 데이터 집합에 포함된 데이터에 수행할 작업을 정의하는 활동의 논리적 그룹화입니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-109">A pipeline is a logical grouping of Activities, each of which defines the actions to perform on the data contained in Datasets.</span></span> <span data-ttu-id="e5aea-110">연결된 서비스는 데이터 팩터리가 데이터 리소스에 연결하기 위해 필요한 정보를 정의하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-110">Linked services are used to define the information needed for Data Factory to connect to the data resources.</span></span>

<span data-ttu-id="e5aea-111">ADF와 함께 기존 데이터 처리 서비스는 가용성이 높고 클라우드에서 관리되는 데이터 파이프라인으로 구성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-111">With ADF, existing data processing services can be composed into data pipelines that are highly available and managed in the cloud.</span></span> <span data-ttu-id="e5aea-112">이러한 데이터 파이프라인에서 데이터 수집, 준비, 변환, 분석 및 게시를 예약할 수 있으며 ADF가 복잡한 데이터 및 처리 종속성을 관리하고 오케스트레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-112">These data pipelines can be scheduled to ingest, prepare, transform, analyze, and publish data, and ADF manages and orchestrates the complex data and processing dependencies.</span></span> <span data-ttu-id="e5aea-113">클라우드에서 솔루션을 신속하게 구축 및 배포할 수 있으며 증가하는 온-프레미스 및 클라우드 데이터 원본을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-113">Solutions can be quickly built and deployed in the cloud, connecting a growing number of on-premises and cloud data sources.</span></span>

<span data-ttu-id="e5aea-114">다음 경우에 ADF 사용을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-114">Consider using ADF:</span></span>

* <span data-ttu-id="e5aea-115">온-프레미스 및 클라우드 리소스 둘 다에 액세스하는 하이브리드 시나리오에서 데이터를 지속적으로 마이그레이션해야 하는 경우</span><span class="sxs-lookup"><span data-stu-id="e5aea-115">when data needs to be continually migrated in a hybrid scenario that accesses both on-premises and cloud resources</span></span>
* <span data-ttu-id="e5aea-116">데이터를 트랜잭션 처리하거나 수정해야 할 때 또는 마이그레이션 중에 비즈니스 논리를 추가할 때</span><span class="sxs-lookup"><span data-stu-id="e5aea-116">when the data is transacted or needs to be modified or have business logic added to it when being migrated.</span></span>

<span data-ttu-id="e5aea-117">ADF에서는 정기적으로 데이터 이동을 관리하는 간단한 JSON 스크립트를 사용하여 작업 예약 및 모니터링이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-117">ADF allows for the scheduling and monitoring of jobs using simple JSON scripts that manage the movement of data on a periodic basis.</span></span> <span data-ttu-id="e5aea-118">또한 복잡한 작업을 지원하는 기타 기능도 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-118">ADF also has other capabilities such as support for complex operations.</span></span> <span data-ttu-id="e5aea-119">ADF에 대한 자세한 내용은 [Azure 데이터 팩터리(ADF)](https://azure.microsoft.com/services/data-factory/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e5aea-119">For more information on ADF, see the documentation at [Azure Data Factory (ADF)](https://azure.microsoft.com/services/data-factory/).</span></span>

## <span data-ttu-id="e5aea-120"><a name="scenario"></a>시나리오</span><span class="sxs-lookup"><span data-stu-id="e5aea-120"><a name="scenario"></a>The Scenario</span></span>
<span data-ttu-id="e5aea-121">두 가지 데이터 마이그레이션 작업을 구성하는 ADF 파이프라인을 설정했습니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-121">We set up an ADF pipeline that composes two data migration activities.</span></span> <span data-ttu-id="e5aea-122">데이터는 매일 온-프레미스 SQL 데이터베이스와 클라우드의 Azure SQL Database 간에 이동됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-122">Together they move data on a daily basis between an on-premises SQL database and an Azure SQL Database in the cloud.</span></span> <span data-ttu-id="e5aea-123">두 활동은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-123">The two activities are:</span></span>

* <span data-ttu-id="e5aea-124">온-프레미스 SQL Server 데이터베이스에서 Azure Blob Storage 계정으로 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="e5aea-124">copy data from an on-premises SQL Server database to an Azure Blob Storage account</span></span>
* <span data-ttu-id="e5aea-125">Azure Blob 저장소 계정에서 Azure SQL 데이터베이스로 데이터 복사</span><span class="sxs-lookup"><span data-stu-id="e5aea-125">copy data from the Azure Blob Storage account to an Azure SQL Database.</span></span>

> [!NOTE]
> <span data-ttu-id="e5aea-126">여기에 나오는 단계는 ADF 팀이 제공한 더 자세한 자습서 [데이터 관리 게이트웨이 클라우드를 사용하여 온-프레미스 원본과 클라우드 간에 데이터 이동](../data-factory/data-factory-move-data-between-onprem-and-cloud.md)을 인용하고 새롭게 구성하였으며 해당하는 경우 해당 항목의 관련 섹션에 대한 참조를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-126">The steps shown here have been adapted from the more detailed tutorial provided by the ADF team: [Move data between on-premises sources and cloud with Data Management Gateway](../data-factory/data-factory-move-data-between-onprem-and-cloud.md) References to the relevant sections of that topic are provided when appropriate.</span></span>
>
>

## <span data-ttu-id="e5aea-127"><a name="prereqs"></a>필수 조건</span><span class="sxs-lookup"><span data-stu-id="e5aea-127"><a name="prereqs"></a>Prerequisites</span></span>
<span data-ttu-id="e5aea-128">이 자습서에서는 사용자가 다음을 보유하고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-128">This tutorial assumes you have:</span></span>

* <span data-ttu-id="e5aea-129">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="e5aea-129">An **Azure subscription**.</span></span> <span data-ttu-id="e5aea-130">구독이 없는 경우 [무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-130">If you do not have a subscription, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="e5aea-131">**Azure 저장소 계정**.</span><span class="sxs-lookup"><span data-stu-id="e5aea-131">An **Azure storage account**.</span></span> <span data-ttu-id="e5aea-132">이 자습서에서는 데이터 저장을 위해 Azure 저장소 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-132">You use an Azure storage account for storing the data in this tutorial.</span></span> <span data-ttu-id="e5aea-133">Azure 저장소 계정이 없는 경우 [저장소 계정 만들기](../storage/common/storage-create-storage-account.md#create-a-storage-account) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e5aea-133">If you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article.</span></span> <span data-ttu-id="e5aea-134">저장소 계정을 만든 후에는 저장소 액세스에 사용되는 계정 키를 확보해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-134">After you have created the storage account, you need to obtain the account key used to access the storage.</span></span> <span data-ttu-id="e5aea-135">[저장소 액세스 키 관리](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e5aea-135">See [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span>
* <span data-ttu-id="e5aea-136">**Azure SQL 데이터베이스**에 대한 액세스.</span><span class="sxs-lookup"><span data-stu-id="e5aea-136">Access to an **Azure SQL Database**.</span></span> <span data-ttu-id="e5aea-137">Azure SQL 데이터베이스를 설정해야 하는 경우, [Microsoft Azure SQL 데이터베이스 시작 ](../sql-database/sql-database-get-started.md) 항목에서 Azure SQL 데이터베이스의 새 인스턴스를 프로비전하는 방법에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-137">If you must set up an Azure SQL Database, the tpoic [Getting Started with Microsoft Azure SQL Database ](../sql-database/sql-database-get-started.md) provides information on how to provision a new instance of an Azure SQL Database.</span></span>
* <span data-ttu-id="e5aea-138">로컬로 설치 및 구성된 **Azure PowerShell** .</span><span class="sxs-lookup"><span data-stu-id="e5aea-138">Installed and configured **Azure PowerShell** locally.</span></span> <span data-ttu-id="e5aea-139">자세한 내용은 [Azure PowerShell 설치 및 구성법](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e5aea-139">For instructions, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

> [!NOTE]
> <span data-ttu-id="e5aea-140">이 절차에서는 [Azure 포털](https://portal.azure.com/)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-140">This procedure uses the [Azure portal](https://portal.azure.com/).</span></span>
>
>

## <span data-ttu-id="e5aea-141"><a name="upload-data"></a> 온-프레미스 SQL Server에 데이터 업로드</span><span class="sxs-lookup"><span data-stu-id="e5aea-141"><a name="upload-data"></a> Upload the data to your on-premises SQL Server</span></span>
<span data-ttu-id="e5aea-142">[NYC Taxi 데이터 집합](http://chriswhong.com/open-data/foil_nyc_taxi/)을 사용하여 마이그레이션 프로세스를 시연합니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-142">We use the [NYC Taxi dataset](http://chriswhong.com/open-data/foil_nyc_taxi/) to demonstrate the migration process.</span></span> <span data-ttu-id="e5aea-143">해당 게시물에서 설명한 것처럼 NYC Taxi 데이터 집합은 Azure Blob Storage [NYC Taxi 데이터](http://www.andresmh.com/nyctaxitrips/)에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-143">The NYC Taxi dataset is available, as noted in that post, on Azure blob storage [NYC Taxi Data](http://www.andresmh.com/nyctaxitrips/).</span></span> <span data-ttu-id="e5aea-144">데이터에는 두 개 파일이 있습니다. trip_data.csv 파일에는 여정 세부 정보가 들어 있고 trip_far.csv 파일에는 각 여정에 대한 요금 세부 정보가 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-144">The data has two files, the trip_data.csv file, which contains trip details, and the  trip_far.csv file, which contains details of the fare paid for each trip.</span></span> <span data-ttu-id="e5aea-145">이러한 파일의 샘플 및 설명은 [NYC Taxi Trips 데이터 집합 설명](machine-learning-data-science-process-sql-walkthrough.md#dataset)에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-145">A sample and description of these files are provided in [NYC Taxi Trips Dataset Description](machine-learning-data-science-process-sql-walkthrough.md#dataset).</span></span>

<span data-ttu-id="e5aea-146">자신의 데이터 집합에 여기에 제공된 절차를 도입하거나 NYC Taxi 데이터 집합을 사용하여 설명된 대로 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-146">You can either adapt the procedure provided here to a set of your own data or follow the steps as described by using the NYC Taxi dataset.</span></span> <span data-ttu-id="e5aea-147">NYC Taxi 데이터 집합을 온-프레미스 SQL Server 데이터베이스에 업로드하려면 [SQL Server Database로 대량 데이터 가져오기](machine-learning-data-science-process-sql-walkthrough.md#dbload)에 설명된 절차를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-147">To upload the NYC Taxi dataset into your on-premises SQL Server database, follow the procedure outlined in [Bulk Import Data into SQL Server Database](machine-learning-data-science-process-sql-walkthrough.md#dbload).</span></span> <span data-ttu-id="e5aea-148">이러한 지침은 Azure Virtual Machine의 SQL Server에 대한 내용이지만 온-프레미스 SQL Server로 업로드하는 절차는 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-148">These instructions are for a SQL Server on an Azure Virtual Machine, but the procedure for uploading to the on-premises SQL Server is the same.</span></span>

## <span data-ttu-id="e5aea-149"><a name="create-adf"></a> Azure 데이터 팩터리 만들기</span><span class="sxs-lookup"><span data-stu-id="e5aea-149"><a name="create-adf"></a> Create an Azure Data Factory</span></span>
<span data-ttu-id="e5aea-150">[Azure Portal](https://portal.azure.com/)에서 새 Azure Data Factory 및 리소스 그룹을 만들기 위한 지침은 [Azure Data Factory 만들기](../data-factory/data-factory-build-your-first-pipeline-using-editor.md#create-data-factory)에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-150">The instructions for creating a new Azure Data Factory and a resource group in the [Azure portal](https://portal.azure.com/) are provided [Create an Azure Data Factory](../data-factory/data-factory-build-your-first-pipeline-using-editor.md#create-data-factory).</span></span> <span data-ttu-id="e5aea-151">새 ADF 인스턴스의 이름은 *adfdsp*이고 생성된 리소스 그룹은 *adfdsprg*입니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-151">Name the new ADF instance *adfdsp* and name the resource group created *adfdsprg*.</span></span>

## <a name="install-and-configure-up-the-data-management-gateway"></a><span data-ttu-id="e5aea-152">데이터 관리 게이트웨이 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="e5aea-152">Install and configure up the Data Management Gateway</span></span>
<span data-ttu-id="e5aea-153">온-프레미스 SQL Server와 작업하도록 Azure Data Factory의 파이프라인을 활성화하려면 데이터 팩터리에 대해 연결된 서비스로 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-153">To enable your pipelines in an Azure data factory to work with an on-premises SQL Server, you need to add it as a Linked Service to the data factory.</span></span> <span data-ttu-id="e5aea-154">온-프레미스 SQL Server에 대한 연결된 서비스를 만들려면 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-154">To create a Linked Service for an on-premises SQL Server, you must:</span></span>

* <span data-ttu-id="e5aea-155">온-프레미스 컴퓨터에 Microsoft 데이터 관리 게이트웨이를 다운로드한 후 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-155">download and install Microsoft Data Management Gateway onto the on-premises computer.</span></span>
* <span data-ttu-id="e5aea-156">온-프레미스 데이터 원본에 대한 연결된 서비스를 게이트웨이를 사용하도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-156">configure the linked service for the on-premises data source to use the gateway.</span></span>

<span data-ttu-id="e5aea-157">데이터 관리 게이트웨이는 호스팅되는 컴퓨터에서 원본 및 싱크 데이터를 직렬화 및 역직렬화합니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-157">The Data Management Gateway serializes and deserializes the source and sink data on the computer where it is hosted.</span></span>

<span data-ttu-id="e5aea-158">데이터 관리 게이트웨이에 대한 설치 지침 및 세부 정보에 대한 내용은 [데이터 관리 게이트웨이 클라우드를 사용하여 온-프레미스 원본과 클라우드 간에 데이터 이동](../data-factory/data-factory-move-data-between-onprem-and-cloud.md)</span><span class="sxs-lookup"><span data-stu-id="e5aea-158">For set-up instructions and details on Data Management Gateway, see [Move data between on-premises sources and cloud with Data Management Gateway](../data-factory/data-factory-move-data-between-onprem-and-cloud.md)</span></span>

## <span data-ttu-id="e5aea-159"><a name="adflinkedservices"></a>데이터 리소스에 연결할 연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="e5aea-159"><a name="adflinkedservices"></a>Create linked services to connect to the data resources</span></span>
<span data-ttu-id="e5aea-160">연결된 서비스는 Azure 데이터 팩터리가 데이터 리소스에 연결하기 위해 필요한 정보를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-160">A linked service defines the information needed for Azure Data Factory to connect to a data resource.</span></span> <span data-ttu-id="e5aea-161">연결된 서비스를 만들기 위한 단계별 절차가 [연결된 서비스 만들기](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-linked-services)에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-161">The step-by-step procedure for creating linked services is provided in [Create linked services](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-linked-services).</span></span>

<span data-ttu-id="e5aea-162">이 시나리오에는 연결된 서비스가 필요한 3개의 리소스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-162">We have three resources in this scenario for which linked services are needed.</span></span>

1. [<span data-ttu-id="e5aea-163">온-프레미스 SQL Server에 대한 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="e5aea-163">Linked service for on-premises SQL Server</span></span>](#adf-linked-service-onprem-sql)
2. [<span data-ttu-id="e5aea-164">Azure Blob 저장소에 대한 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="e5aea-164">Linked service for Azure Blob Storage</span></span>](#adf-linked-service-blob-store)
3. [<span data-ttu-id="e5aea-165">Azure SQL 데이터베이스에 대한 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="e5aea-165">Linked service for Azure SQL database</span></span>](#adf-linked-service-azure-sql)

### <span data-ttu-id="e5aea-166"><a name="adf-linked-service-onprem-sql"></a>온-프레미스 SQL Server 데이터베이스에 대한 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="e5aea-166"><a name="adf-linked-service-onprem-sql"></a>Linked service for on-premises SQL Server database</span></span>
<span data-ttu-id="e5aea-167">온-프레미스 SQL Server에 대한 연결된 서비스를 만들려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-167">To create the linked service for the on-premises SQL Server:</span></span>

* <span data-ttu-id="e5aea-168">Azure 클래식 포털의 ADF 방문 페이지에서 **데이터 저장소**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-168">click the **Data Store** in the ADF landing page on Azure Classic Portal</span></span>
* <span data-ttu-id="e5aea-169">**SQL**을 선택하고 온-프레미스 SQL Server에 대한 *사용자 이름* 및 *암호* 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-169">select **SQL** and enter the *username* and *password* credentials for the on-premises SQL Server.</span></span> <span data-ttu-id="e5aea-170">servername을 **정규화된 서버 이름 백슬래시 인스턴스 이름(servername\instancename)**으로 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-170">You need to enter the servername as a **fully qualified servername backslash instance name (servername\instancename)**.</span></span> <span data-ttu-id="e5aea-171">연결된 서비스 이름을 *adfonpremsql*로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-171">Name the linked service *adfonpremsql*.</span></span>

### <span data-ttu-id="e5aea-172"><a name="adf-linked-service-blob-store"></a>Blob에 대한 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="e5aea-172"><a name="adf-linked-service-blob-store"></a>Linked service for Blob</span></span>
<span data-ttu-id="e5aea-173">Azure Blob 저장소 계정에 대한 연결된 서비스를 만들려면</span><span class="sxs-lookup"><span data-stu-id="e5aea-173">To create the linked service for the Azure Blob Storage account:</span></span>

* <span data-ttu-id="e5aea-174">Azure 클래식 포털의 ADF 방문 페이지에서 **데이터 저장소** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-174">click the **Data Store** in the ADF landing page on Azure Classic Portal</span></span>
* <span data-ttu-id="e5aea-175">**Azure Storage Account**</span><span class="sxs-lookup"><span data-stu-id="e5aea-175">select **Azure Storage Account**</span></span>
* <span data-ttu-id="e5aea-176">Azure Blob 저장소 계정 키 및 컨테이너 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-176">enter the Azure Blob Storage account key and container name.</span></span> <span data-ttu-id="e5aea-177">연결된 서비스 이름을 *adfds*로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-177">Name the Linked Service *adfds*.</span></span>

### <span data-ttu-id="e5aea-178"><a name="adf-linked-service-azure-sql"></a>Azure SQL 데이터베이스에 대한 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="e5aea-178"><a name="adf-linked-service-azure-sql"></a>Linked service for Azure SQL database</span></span>
<span data-ttu-id="e5aea-179">Azure SQL 데이터베이스에 대한 연결된 서비스를 만들려면</span><span class="sxs-lookup"><span data-stu-id="e5aea-179">To create the linked service for the Azure SQL Database:</span></span>

* <span data-ttu-id="e5aea-180">Azure 클래식 포털의 ADF 방문 페이지에서 **데이터 저장소** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-180">click the **Data Store** in the ADF landing page on Azure Classic Portal</span></span>
* <span data-ttu-id="e5aea-181">**Azure SQL**을 선택하고 Azure SQL Database에 대한 *사용자 이름* 및 *암호* 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-181">select **Azure SQL** and enter the *username* and *password* credentials for the Azure SQL Database.</span></span> <span data-ttu-id="e5aea-182">*사용자 이름*은 *user@servername*으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-182">The *username* must be specified as *user@servername*.</span></span>   

## <span data-ttu-id="e5aea-183"><a name="adf-tables"></a>데이터 집합에 액세스하는 방법을 지정하는 테이블 정의 및 만들기</span><span class="sxs-lookup"><span data-stu-id="e5aea-183"><a name="adf-tables"></a>Define and create tables to specify how to access the datasets</span></span>
<span data-ttu-id="e5aea-184">다음 스크립트 기반 프로시저로 데이터 집합의 구조, 위치 및 가용성을 지정하는 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-184">Create tables that specify the structure, location, and availability of the datasets with the following script-based procedures.</span></span> <span data-ttu-id="e5aea-185">테이블을 정의하는 데 JSON 파일이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-185">JSON files are used to define the tables.</span></span> <span data-ttu-id="e5aea-186">이러한 파일의 구조에 대한 자세한 내용은 [데이터 집합](../data-factory/data-factory-create-datasets.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e5aea-186">For more information on the structure of these files, see [Datasets](../data-factory/data-factory-create-datasets.md).</span></span>

> [!NOTE]
> <span data-ttu-id="e5aea-187">[New-AzureDataFactoryTable](https://msdn.microsoft.com/library/azure/dn835096.aspx) cmdlet을 실행하기 전에 `Add-AzureAccount` cmdlet을 실행하여 명령 실행을 위해 Azure 구독을 선택했는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-187">You should execute the `Add-AzureAccount` cmdlet before executing the [New-AzureDataFactoryTable](https://msdn.microsoft.com/library/azure/dn835096.aspx) cmdlet to confirm that the right Azure subscription is selected for the command execution.</span></span> <span data-ttu-id="e5aea-188">이 cmdlet의 설명서는 [Add-azureaccount](/powershell/module/azure/add-azureaccount?view=azuresmps-3.7.0)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e5aea-188">For documentation of this cmdlet, see [Add-AzureAccount](/powershell/module/azure/add-azureaccount?view=azuresmps-3.7.0).</span></span>
>
>

<span data-ttu-id="e5aea-189">테이블에서 JSON 기반 정의는 다음 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-189">The JSON-based definitions in the tables use the following names:</span></span>

* <span data-ttu-id="e5aea-190">온-프레미스 SQL Server의 **테이블 이름**은 *nyctaxi_data*</span><span class="sxs-lookup"><span data-stu-id="e5aea-190">the **table name** in the on-premises SQL server is *nyctaxi_data*</span></span>
* <span data-ttu-id="e5aea-191">the **컨테이너 이름** 은 *containername*</span><span class="sxs-lookup"><span data-stu-id="e5aea-191">the **container name** in the Azure Blob Storage account is *containername*</span></span>  

<span data-ttu-id="e5aea-192">이 ADF 파이프라인에는 3개의 테이블 정의가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-192">Three table definitions are needed for this ADF pipeline:</span></span>

1. [<span data-ttu-id="e5aea-193">SQL 온-프레미스 테이블</span><span class="sxs-lookup"><span data-stu-id="e5aea-193">SQL on-premises Table</span></span>](#adf-table-onprem-sql)
2. [<span data-ttu-id="e5aea-194">Blob 테이블 </span><span class="sxs-lookup"><span data-stu-id="e5aea-194">Blob Table </span></span>](#adf-table-blob-store)
3. [<span data-ttu-id="e5aea-195">SQL Azure 테이블</span><span class="sxs-lookup"><span data-stu-id="e5aea-195">SQL Azure Table</span></span>](#adf-table-azure-sql)

> [!NOTE]
> <span data-ttu-id="e5aea-196">이러한 절차에서는 Azure PowerShell을 사용하여 ADF 활동을 정의하고 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-196">These procedures use Azure PowerShell to define and create the ADF activities.</span></span> <span data-ttu-id="e5aea-197">그러나 이러한 작업은 Azure 포털을 사용해서도 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-197">But these tasks can also be accomplished using the Azure portal.</span></span> <span data-ttu-id="e5aea-198">자세한 내용은 [데이터 집합 만들기](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-datasets)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e5aea-198">For details, see [Create datasets](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-datasets).</span></span>
>
>

### <span data-ttu-id="e5aea-199"><a name="adf-table-onprem-sql"></a>SQL 온-프레미스 테이블</span><span class="sxs-lookup"><span data-stu-id="e5aea-199"><a name="adf-table-onprem-sql"></a>SQL on-premises Table</span></span>
<span data-ttu-id="e5aea-200">온-프레미스 SQL Server에 대한 테이블 정의는 다음 JSON 파일에 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-200">The table definition for the on-premises SQL Server is specified in the following JSON file:</span></span>

        {
            "name": "OnPremSQLTable",
            "properties":
            {
                "location":
                {
                "type": "OnPremisesSqlServerTableLocation",
                "tableName": "nyctaxi_data",
                "linkedServiceName": "adfonpremsql"
                },
                "availability":
                {
                "frequency": "Day",
                "interval": 1,   
                "waitOnExternal":
                {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
                }

                }
            }
        }

<span data-ttu-id="e5aea-201">여기서는 열 이름이 포함되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-201">The column names were not included here.</span></span> <span data-ttu-id="e5aea-202">여기에 열 이름을 포함하여 열 이름을 sub-select할 수 있습니다(자세한 내용은 [ADF 설명서](../data-factory/data-factory-data-movement-activities.md) 항목 참조).</span><span class="sxs-lookup"><span data-stu-id="e5aea-202">You can sub-select on the column names by including them here (for details check the [ADF documentation](../data-factory/data-factory-data-movement-activities.md) topic.</span></span>

<span data-ttu-id="e5aea-203">테이블의 JSON 정의를 *onpremtabledef.json* 파일로 복사하고 알려진 위치에 저장합니다(여기서는 *C:\temp\onpremtabledef.json*으로 간주).</span><span class="sxs-lookup"><span data-stu-id="e5aea-203">Copy the JSON definition of the table into a file called *onpremtabledef.json* file and save it to a known location (here assumed to be *C:\temp\onpremtabledef.json*).</span></span> <span data-ttu-id="e5aea-204">다음 Azure PowerShell cmdlet을 사용하여 ADF에 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-204">Create the table in ADF with the following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryTable -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp –File C:\temp\onpremtabledef.json


### <span data-ttu-id="e5aea-205"><a name="adf-table-blob-store"></a>Blob 테이블</span><span class="sxs-lookup"><span data-stu-id="e5aea-205"><a name="adf-table-blob-store"></a>Blob Table</span></span>
<span data-ttu-id="e5aea-206">출력 blob 위치에 대한 테이블 정의는 다음과 같습니다(온-프레미스에서 수집된 데이터를 Azure blob에 매핑).</span><span class="sxs-lookup"><span data-stu-id="e5aea-206">Definition for the table for the output blob location is in the following (this maps the ingested data from on-premises to Azure blob):</span></span>

        {
            "name": "OutputBlobTable",
            "properties":
            {
                "location":
                {
                "type": "AzureBlobLocation",
                "folderPath": "containername",
                "format":
                {
                "type": "TextFormat",
                "columnDelimiter": "\t"
                },
                "linkedServiceName": "adfds"
                },
                "availability":
                {
                "frequency": "Day",
                "interval": 1
                }
            }
        }

<span data-ttu-id="e5aea-207">테이블의 JSON 정의를 *bloboutputtabledef.json* 파일로 복사하고 알려진 위치에 저장합니다(여기서는 *C:\temp\bloboutputtabledef.json*으로 간주).</span><span class="sxs-lookup"><span data-stu-id="e5aea-207">Copy the JSON definition of the table into a file called *bloboutputtabledef.json* file and save it to a known location (here assumed to be *C:\temp\bloboutputtabledef.json*).</span></span> <span data-ttu-id="e5aea-208">다음 Azure PowerShell cmdlet을 사용하여 ADF에 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-208">Create the table in ADF with the following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\bloboutputtabledef.json  

### <span data-ttu-id="e5aea-209"><a name="adf-table-azure-sq"></a>SQL Azure 테이블</span><span class="sxs-lookup"><span data-stu-id="e5aea-209"><a name="adf-table-azure-sq"></a>SQL Azure Table</span></span>
<span data-ttu-id="e5aea-210">SQL Azure 출력에 대한 테이블 정의가 다음과 같습니다(이 스키마는 blob에서 가져온 데이터를 매핑).</span><span class="sxs-lookup"><span data-stu-id="e5aea-210">Definition for the table for the SQL Azure output is in the following (this schema maps the data coming from the blob):</span></span>

    {
        "name": "OutputSQLAzureTable",
        "properties":
        {
            "structure":
            [
                { "name": "column1", type": "String"},
                { "name": "column2", type": "String"}                
            ],
            "location":
            {
                "type": "AzureSqlTableLocation",
                "tableName": "your_db_name",
                "linkedServiceName": "adfdssqlazure_linked_servicename"
            },
            "availability":
            {
                "frequency": "Day",
                "interval": 1            
            }
        }
    }

<span data-ttu-id="e5aea-211">테이블의 JSON 정의를 *AzureSqlTable.json*이라는 파일로 복사하고 알려진 위치에 저장합니다(여기서는 *C:\temp\AzureSqlTable.json*으로 간주).</span><span class="sxs-lookup"><span data-stu-id="e5aea-211">Copy the JSON definition of the table into a file called *AzureSqlTable.json* file and save it to a known location (here assumed to be *C:\temp\AzureSqlTable.json*).</span></span> <span data-ttu-id="e5aea-212">다음 Azure PowerShell cmdlet을 사용하여 ADF에 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-212">Create the table in ADF with the following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\AzureSqlTable.json  


## <span data-ttu-id="e5aea-213"><a name="adf-pipeline"></a>파이프라인 정의 및 만들기</span><span class="sxs-lookup"><span data-stu-id="e5aea-213"><a name="adf-pipeline"></a>Define and create the pipeline</span></span>
<span data-ttu-id="e5aea-214">파이프라인에 포함될 활동을 지정하고 다음 스크립트 기반 프로시저로 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-214">Specify the activities that belong to the pipeline and create the pipeline with the following script-based procedures.</span></span> <span data-ttu-id="e5aea-215">파이프라인 속성을 정의하는 데 JSON 파일이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-215">A JSON file is used to define the pipeline properties.</span></span>

* <span data-ttu-id="e5aea-216">스크립트는 **파이프라인 이름** 이 *AMLDSProcessPipeline*이라고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-216">The script assumes that the **pipeline name** is *AMLDSProcessPipeline*.</span></span>
* <span data-ttu-id="e5aea-217">또한 파이프라인이 매일 정기적으로 실행되도록 파이프라인의 주기성을 설정하고 작업에 대한 기본 실행 시간을 사용합니다(오전 12시 UTC).</span><span class="sxs-lookup"><span data-stu-id="e5aea-217">Also note that we set the periodicity of the pipeline to be executed on daily basis and use the default execution time for the job (12 am UTC).</span></span>

> [!NOTE]
> <span data-ttu-id="e5aea-218">다음 절차에서는 Azure PowerShell을 사용하여 ADF 파이프라인을 정의하고 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-218">The following procedures use Azure PowerShell to define and create the ADF pipeline.</span></span> <span data-ttu-id="e5aea-219">그러나 이러한 작업은 Azure 포털을 사용해서도 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-219">But this task can also be accomplished using the Azure portal.</span></span> <span data-ttu-id="e5aea-220">자세한 내용은 [파이프라인 만들기](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-pipeline)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e5aea-220">For details, see [Create pipeline](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-pipeline).</span></span>
>
>

<span data-ttu-id="e5aea-221">이전에 제공된 테이블 정의를 사용하여 ADF에 대한 파이프라인 정의는 다음과 같이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-221">Using the table definitions provided previously, the pipeline definition for the ADF is specified as follows:</span></span>

        {
            "name": "AMLDSProcessPipeline",
            "properties":
            {
                "description" : "This pipeline has one Copy activity that copies data from an on-premises SQL to Azure blob",
                 "activities":
                [
                    {
                        "name": "CopyFromSQLtoBlob",
                        "description": "Copy data from on-premises SQL server to blob",     
                        "type": "CopyActivity",
                        "inputs": [ {"name": "OnPremSQLTable"} ],
                        "outputs": [ {"name": "OutputBlobTable"} ],
                        "transformation":
                        {
                            "source":
                            {                               
                                "type": "SqlSource",
                                "sqlReaderQuery": "select * from nyctaxi_data"
                            },
                            "sink":
                            {
                                "type": "BlobSink"
                            }   
                        },
                        "Policy":
                        {
                            "concurrency": 3,
                            "executionPriorityOrder": "NewestFirst",
                            "style": "StartOfInterval",
                            "retry": 0,
                            "timeout": "01:00:00"
                        }       

                     },

                    {
                        "name": "CopyFromBlobtoSQLAzure",
                        "description": "Push data to Sql Azure",        
                        "type": "CopyActivity",
                        "inputs": [ {"name": "OutputBlobTable"} ],
                        "outputs": [ {"name": "OutputSQLAzureTable"} ],
                        "transformation":
                        {
                            "source":
                            {                               
                                "type": "BlobSource"
                            },
                            "sink":
                            {
                                "type": "SqlSink",
                                "WriteBatchTimeout": "00:5:00",                
                            }            
                        },
                        "Policy":
                        {
                            "concurrency": 3,
                            "executionPriorityOrder": "NewestFirst",
                            "style": "StartOfInterval",
                            "retry": 2,
                            "timeout": "02:00:00"
                        }
                     }
                ]
            }
        }

<span data-ttu-id="e5aea-222">파이프라인의 이 JSON 정의를 *pipelinedef.json* 파일로 복사하고 알려진 위치에 저장합니다(여기서는 *C:\temp\pipelinedef.json*으로 간주).</span><span class="sxs-lookup"><span data-stu-id="e5aea-222">Copy this JSON definition of the pipeline into a file called *pipelinedef.json* file and save it to a known location (here assumed to be *C:\temp\pipelinedef.json*).</span></span> <span data-ttu-id="e5aea-223">다음 Azure PowerShell cmdlet을 사용하여 ADF에 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-223">Create the pipeline in ADF with the following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryPipeline  -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\pipelinedef.json

<span data-ttu-id="e5aea-224">Azure 클래식 포털의 ADF에서 다음과 같이 파이프라인이 표시되는지 확인합니다(다이어그램을 클릭할 때).</span><span class="sxs-lookup"><span data-stu-id="e5aea-224">Confirm that you can see the pipeline on the ADF in the Azure Classic Portal show up as following (when you click the diagram)</span></span>

![ADF 파이프라인](media/machine-learning-data-science-move-sql-azure-adf/DJP1kji.png)

## <span data-ttu-id="e5aea-226"><a name="adf-pipeline-start"></a>파이프라인 시작</span><span class="sxs-lookup"><span data-stu-id="e5aea-226"><a name="adf-pipeline-start"></a>Start the Pipeline</span></span>
<span data-ttu-id="e5aea-227">이제 다음 명령을 사용하여 파이프라인을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-227">The pipeline can now be run using the following command:</span></span>

    Set-AzureDataFactoryPipelineActivePeriod -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp -StartDateTime startdateZ –EndDateTime enddateZ –Name AMLDSProcessPipeline

<span data-ttu-id="e5aea-228">*startdate* 및 *enddate* 매개 변수 값을 파이프라인을 실행할 실제 날짜로 바꿔야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-228">The *startdate* and *enddate* parameter values need to be replaced with the actual dates between which you want the pipeline to run.</span></span>

<span data-ttu-id="e5aea-229">파이프라인이 실행된 후에는 blob에 대해 선택한 컨테이너에 표시된 데이터를 하루에 한 개 파일로 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-229">Once the pipeline executes, you should be able to see the data show up in the container selected for the blob, one file per day.</span></span>

<span data-ttu-id="e5aea-230">데이터를 증분 방식으로 파이프하는 ADF 제공 기능을 활용하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="e5aea-230">Note that we have not leveraged the functionality provided by ADF to pipe data incrementally.</span></span> <span data-ttu-id="e5aea-231">이 작업을 수행하는 방법 및 ADF에서 제공하는 기타 기능에 대한 자세한 내용은 [ADF 설명서](https://azure.microsoft.com/services/data-factory/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e5aea-231">For more information on how to do this and other capabilities provided by ADF, see the [ADF documentation](https://azure.microsoft.com/services/data-factory/).</span></span>
