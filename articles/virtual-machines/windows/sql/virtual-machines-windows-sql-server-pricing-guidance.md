---
title: "Azure Virtual Machines의 SQL Server에 대한 효과적인 비용 관리 | Microsoft 문서"
description: "적합한 SQL Server 가상 컴퓨터 가격 책정 모델을 선택하기 위한 모범 사례를 제공합니다."
services: virtual-machines-windows
documentationcenter: na
author: luisherring
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 04/18/2017
ms.author: jroth
ms.openlocfilehash: 29a92f0c70bffedeb75c50b7fc3b687ee5ee227d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="pricing-guidance-for-sql-server-azure-vms"></a><span data-ttu-id="34c32-103">SQL Server Azure VM에 대한 가격 책정 지침</span><span class="sxs-lookup"><span data-stu-id="34c32-103">Pricing guidance for SQL Server Azure VMs</span></span>

<span data-ttu-id="34c32-104">이 항목에서는 Azure의 SQL Server 가상 컴퓨터에 대한 가격 책정 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="34c32-104">This topic provides pricing guidance for SQL Server virtual machines in Azure.</span></span> <span data-ttu-id="34c32-105">비용에 영향을 미치는 다양한 옵션이 있고 비용과 비즈니스 요구 사항 간에 균형을 이루는 적합한 이미지를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c32-105">There are several options that affect cost, and it is important to pick the right image that balances costs with business requirements.</span></span>

## <a name="free-licensed-sql-server-editions"></a><span data-ttu-id="34c32-106">무료 라이선스 SQL Server 버전</span><span class="sxs-lookup"><span data-stu-id="34c32-106">Free-licensed SQL Server editions</span></span>

<span data-ttu-id="34c32-107">개념 증명을 개발, 테스트 또는 빌드하려면 무료 라이선스 **SQL Server Developer Edition**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="34c32-107">If you want to develop, test, or build a proof of concept, then use the free-licensed **SQL Server Developer edition**.</span></span> <span data-ttu-id="34c32-108">이 버전에는 SQL Server Enterprise Edition의 모든 기능이 포함되므로 원하는 모든 응용 프로그램을 빌드하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34c32-108">This edition has everything in SQL Server Enterprise edition, thus you can use it to build whatever application you want.</span></span> <span data-ttu-id="34c32-109">프로덕션에서는 실행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="34c32-109">It’s just not allowed to run in production.</span></span> <span data-ttu-id="34c32-110">SQL Server Developer VM의 경우 SQL Server 라이선스가 아닌 VM에 대한 비용만 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="34c32-110">A SQL Server Developer VM will only charge for the cost of the VM, not for SQL Server licensing.</span></span>

<span data-ttu-id="34c32-111">프로덕션에서 간단한 작업을 실행하려면(<4개 코어, <1GB 메모리, <10GB/데이터베이스) 무료 라이선스 **SQL Server Express Edition**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="34c32-111">If you want to run a lightweight workload in production (<4 cores, <1 GB memory, <10 GB/database), then use the free-licensed **SQL Server Express edition**.</span></span> <span data-ttu-id="34c32-112">SQL Express VM의 경우 SQL 라이선스가 아닌 VM에 대한 비용만 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="34c32-112">A SQL Express VM will only charge for the cost of the VM, not SQL licensing.</span></span>

<span data-ttu-id="34c32-113">이러한 개발/테스트 또는 간단한 프로덕션 작업의 경우 이러한 작업에 맞는 더 작은 VM 크기를 선택하여 비용을 절감할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34c32-113">For these development/test or lightweight production workloads, you can also save money by choosing a smaller VM size that matches these workloads.</span></span> <span data-ttu-id="34c32-114">이러한 작업에는 DS1v2를 선택하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="34c32-114">The DS1v2 might be a good choice for these workloads.</span></span>

<span data-ttu-id="34c32-115">이러한 이미지 중 하나를 사용하여 SQL Server 2016 Azure VM을 만들려면 다음 링크를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="34c32-115">To create a SQL Server 2016 Azure VM with one of these images, see the following links:</span></span>

- [<span data-ttu-id="34c32-116">SQL Server 2016 Developer Azure VM</span><span class="sxs-lookup"><span data-stu-id="34c32-116">SQL Server 2016 Developer Azure VM</span></span>](https://ms.portal.azure.com/#create/Microsoft.FreeLicenseSQLServer2016SP1DeveloperWindowsServer2016-ARM)
- [<span data-ttu-id="34c32-117">SQL Server 2016 Express Azure VM</span><span class="sxs-lookup"><span data-stu-id="34c32-117">SQL Server 2016 Express Azure VM</span></span>](https://ms.portal.azure.com/#create/Microsoft.FreeLicenseSQLServer2016SP1ExpressWindowsServer2016-ARM)

## <a name="paid-sql-server-editions"></a><span data-ttu-id="34c32-118">유료 SQL Server 버전</span><span class="sxs-lookup"><span data-stu-id="34c32-118">Paid SQL Server editions</span></span>

<span data-ttu-id="34c32-119">복잡한 프로덕션 작업이 있는 경우 다음 SQL Server 버전 중 하나를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="34c32-119">If you have a non-lightweight production workload, use one of the following SQL Server editions:</span></span>

| <span data-ttu-id="34c32-120">SQL Server 버전</span><span class="sxs-lookup"><span data-stu-id="34c32-120">SQL Server Edition</span></span> | <span data-ttu-id="34c32-121">워크로드</span><span class="sxs-lookup"><span data-stu-id="34c32-121">Workload</span></span> |
|-----|-----|
| <span data-ttu-id="34c32-122">웹</span><span class="sxs-lookup"><span data-stu-id="34c32-122">Web</span></span> | <span data-ttu-id="34c32-123">작은 웹 사이트</span><span class="sxs-lookup"><span data-stu-id="34c32-123">Small web sites</span></span> |
| <span data-ttu-id="34c32-124">Standard</span><span class="sxs-lookup"><span data-stu-id="34c32-124">Standard</span></span> | <span data-ttu-id="34c32-125">소규모~중간 규모 작업</span><span class="sxs-lookup"><span data-stu-id="34c32-125">Small to medium workloads</span></span> |
| <span data-ttu-id="34c32-126">Enterprise</span><span class="sxs-lookup"><span data-stu-id="34c32-126">Enterprise</span></span> | <span data-ttu-id="34c32-127">대규모 또는 중요 업무용 작업</span><span class="sxs-lookup"><span data-stu-id="34c32-127">Large or mission-critical workloads</span></span>|

<span data-ttu-id="34c32-128">이러한 버전의 SQL Server 라이선스 요금을 지급하는 두 가지 옵션은 *사용당 지급* 또는 *사용자 라이선스 필요*입니다.</span><span class="sxs-lookup"><span data-stu-id="34c32-128">You have two options to pay for SQL Server licensing for these editions: *pay per usage* or *bring your own license*.</span></span>

### <a name="pay-per-usage"></a><span data-ttu-id="34c32-129">사용당 지급</span><span class="sxs-lookup"><span data-stu-id="34c32-129">Pay per usage</span></span>

<span data-ttu-id="34c32-130">**사용당 SQL Server 라이선스 지급**은 Azure VM의 분당 비용에 SQL Server 라이선스 비용이 포함됨을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="34c32-130">**Paying the SQL Server license per usage** means that the per-minute cost of running the Azure VM includes the cost of the SQL Server license.</span></span> <span data-ttu-id="34c32-131">[Azure VM 가격 페이지](https://azure.microsoft.com/pricing/details/virtual-machines/sql-server-standard)에서 다른 SQL Server 버전(Web, Standard, Enterprise)에 대한 가격을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34c32-131">You can see the pricing for the different SQL Server editions (Web, Standard, Enterprise) in the [Azure VM pricing page](https://azure.microsoft.com/pricing/details/virtual-machines/sql-server-standard).</span></span> <span data-ttu-id="34c32-132">SQL Server의 모든 버전(2008 R2~2016)에 대한 비용은 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="34c32-132">The cost is the same for all versions of SQL Server (2008 R2 to 2016).</span></span> <span data-ttu-id="34c32-133">일반적으로 SQL Server 라이선스처럼 분당 라이선스 비용은 VM 코어 수에 따라 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="34c32-133">As with SQL Server licensing in general, the per-minute licensing cost depends on the number of VM cores.</span></span>

<span data-ttu-id="34c32-134">사용당 SQL Server 라이선스 지급이 권장되는 경우는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="34c32-134">Paying the SQL Server licensing per usage is recommended for:</span></span>

- <span data-ttu-id="34c32-135">임시 또는 정기적인 작업.</span><span class="sxs-lookup"><span data-stu-id="34c32-135">Temporary or periodic workloads.</span></span> <span data-ttu-id="34c32-136">예: 매주 월요일의 비즈니스 분석 또는 1년에 몇 개월 동안 이벤트를 지원해야 하는 앱.</span><span class="sxs-lookup"><span data-stu-id="34c32-136">For example, an app that needs to support an event for a couple of months every year, or business analysis on Mondays.</span></span>
- <span data-ttu-id="34c32-137">수명 또는 규모를 알 수 없는 작업.</span><span class="sxs-lookup"><span data-stu-id="34c32-137">Workloads with unknown lifetime or scale.</span></span> <span data-ttu-id="34c32-138">예: 몇 개월 내에 필요하지 않을 수 있거나 수요에 따라 더 많은 또는 더 적은 계산 기능이 필요할 수 있는 앱.</span><span class="sxs-lookup"><span data-stu-id="34c32-138">For example, an app that may not be required in a few months, or which may require more, or less compute power, depending on demand.</span></span>

<span data-ttu-id="34c32-139">이러한 사용당 지급 이미지 중 하나를 사용하여 SQL Server 2016 Azure VM을 만들려면 다음 링크를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="34c32-139">To create a SQL Server 2016 Azure VM with one of these pay-per-usage images, see the following links:</span></span>

- [<span data-ttu-id="34c32-140">SQL Server 2016 Web Azure VM</span><span class="sxs-lookup"><span data-stu-id="34c32-140">SQL Server 2016 Web Azure VM</span></span>](https://ms.portal.azure.com/#create/Microsoft.SQLServer2016SP1WebWindowsServer2016)
- [<span data-ttu-id="34c32-141">SQL Server 2016 Standard Azure VM</span><span class="sxs-lookup"><span data-stu-id="34c32-141">SQL Server 2016 Standard Azure VM</span></span>](https://ms.portal.azure.com/#create/Microsoft.SQLServer2016SP1StandardWindowsServer2016)
- [<span data-ttu-id="34c32-142">SQL Server 2016 Enterprise Azure VM</span><span class="sxs-lookup"><span data-stu-id="34c32-142">SQL Server 2016 Enterprise Azure VM</span></span>](https://ms.portal.azure.com/#create/Microsoft.SQLServer2016SP1EnterpriseWindowsServer2016)

> [!IMPORTANT]
> <span data-ttu-id="34c32-143">Azure Portal에서 SQL Server 가상 컴퓨터를 만들 경우 **크기 선택** 블레이드에 표시된 월별 예상 비용에는 SQL Server 라이선스 비용이 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="34c32-143">When you create a SQL Server virtual machine in the Azure portal, the estimated monthly cost displayed on the **Choose a size** blade does not include SQL Server licensing costs.</span></span> <span data-ttu-id="34c32-144">이것은 VM만의 비용입니다.</span><span class="sxs-lookup"><span data-stu-id="34c32-144">This is the cost of the VM alone.</span></span>
>
> ![VM 크기 선택 블레이드](./media/virtual-machines-windows-sql-server-pricing-guidance/sql-vm-choose-size-pricing-estimate.png)
>
><span data-ttu-id="34c32-146">SQL Server의 무료 라이선스 Express 및 Developer 버전의 경우, 이것은 총 예상 비용입니다.</span><span class="sxs-lookup"><span data-stu-id="34c32-146">For the free-licensed Express and Developer editions of SQL Server, this is the total estimated cost.</span></span> <span data-ttu-id="34c32-147">하지만 Web, Standard 및 Enterprise의 경우 [Windows 가상 컴퓨터 가격](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) 페이지에서 추가적인 SQL 라이선스 비용을 찾아보세요.</span><span class="sxs-lookup"><span data-stu-id="34c32-147">But for Web, Standard, and Enterprise, find the additional SQL licensing costs on the [Windows Virtual Machines pricing page](https://azure.microsoft.com/pricing/details/virtual-machines/windows/).</span></span> <span data-ttu-id="34c32-148">가격 페이지에서 SQL Server의 대상 버전을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="34c32-148">On the pricing page, select your target edition of SQL Server.</span></span>

### <a name="bring-your-own-license-byol"></a><span data-ttu-id="34c32-149">BYOL(사용자 라이선스 필요)</span><span class="sxs-lookup"><span data-stu-id="34c32-149">Bring your own license (BYOL)</span></span>

<span data-ttu-id="34c32-150">**License Mobility를 통해 SQL Server 사용자 라이선스 필요**(**BYOL**이라고도 함)는 Azure VM에서 기존 SQL Server 볼륨 라이선스와 함께 Software Assurance를 사용함을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="34c32-150">**Bringing your own SQL Server license through License Mobility**, also referred to as **BYOL**, means using an existing SQL Server Volume License with Software Assurance in an Azure VM.</span></span> <span data-ttu-id="34c32-151">BYOL을 사용하는 SQL Server VM의 경우 볼륨 라이선싱 프로그램을 통해 이미 라이선스 및 Software Assurance를 구매했다면 SQL Server 라이선스가 아닌 VM 실행에 대한 비용만 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="34c32-151">A SQL Server VM using BYOL will only charge for the cost of running the VM, not for SQL Server licensing, given that you have already acquired licenses and Software Assurance through a Volume Licensing program.</span></span>

<span data-ttu-id="34c32-152">License Mobility를 통한 SQL 사용자 라이선스 필요가 권장되는 경우는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="34c32-152">Bringing your own SQL licensing through License Mobility is recommended for:</span></span>

- <span data-ttu-id="34c32-153">연속 작업.</span><span class="sxs-lookup"><span data-stu-id="34c32-153">Continuous workloads.</span></span> <span data-ttu-id="34c32-154">예: 연중무휴 비즈니스 작업을 지원해야 하는 앱.</span><span class="sxs-lookup"><span data-stu-id="34c32-154">For example, an app that needs to support business operations 24x7.</span></span>
- <span data-ttu-id="34c32-155">수명 또는 규모가 알려진 작업.</span><span class="sxs-lookup"><span data-stu-id="34c32-155">Workloads with known lifetime and scale.</span></span> <span data-ttu-id="34c32-156">예: 1년 내내 필요하고 수요가 예측된 앱.</span><span class="sxs-lookup"><span data-stu-id="34c32-156">For example, an app that will be required for the whole year and which demand has been forecasted.</span></span>

<span data-ttu-id="34c32-157">BYOL과 함께 SQL Server VM을 사용하려면 SQL Server Standard 또는 Enterprise에 대한 라이선스와 함께 일부 [Volume Licensing](https://www.microsoft.com/en-us/download/details.aspx?id=10585)(볼륨 라이선싱) 프로그램을 통한 필수 옵션이자 다른 프로그램에 대한 선택적 구매인 [Software Assurance](https://www.microsoft.com/en-us/licensing/licensing-programs/software-assurance-default.aspx#tab=1)가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c32-157">To use BYOL with a SQL Server VM, you must have a license for SQL Server Standard or Enterprise and [Software Assurance](https://www.microsoft.com/en-us/licensing/licensing-programs/software-assurance-default.aspx#tab=1), which is a required option through some [Volume Licensing](https://www.microsoft.com/en-us/download/details.aspx?id=10585) programs and an optional purchase with others.</span></span>  <span data-ttu-id="34c32-158">볼륨 라이선싱을 통해 제공된 가격 수준은 SQL Server에 대한 계약 유형과 수량 및/또는 약정에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="34c32-158">The pricing levels provided through Volume Licensing programs varies, based on the type of agreement and the quantity and or commitment to SQL Server.</span></span> <span data-ttu-id="34c32-159">하지만 일반적으로 연속 프로덕션 작업에 대한 사용자 라이선스 필요에는 다음과 같은 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34c32-159">But as a rule of thumb, bringing your own license for continuous production workloads has the following benefits:</span></span>

| <span data-ttu-id="34c32-160">BYOL 이점</span><span class="sxs-lookup"><span data-stu-id="34c32-160">BYOL benefit</span></span> | <span data-ttu-id="34c32-161">설명</span><span class="sxs-lookup"><span data-stu-id="34c32-161">Description</span></span> |
|-----|-----|
| <span data-ttu-id="34c32-162">**비용 절감**</span><span class="sxs-lookup"><span data-stu-id="34c32-162">**Cost savings**</span></span> | <span data-ttu-id="34c32-163">작업에서 SQL Server Standard 또는 Enterprise를 *10개월 넘게* 연속적으로 실행할 경우 SQL Server 사용자 라이선스 필요가 사용당 지급보다 더 비용 효과적입니다.</span><span class="sxs-lookup"><span data-stu-id="34c32-163">Bringing your own SQL Server license is more cost effective than paying it per usage if a workload will run continuously SQL Server Standard or Enterprise for *more than 10 months*.</span></span> |
| <span data-ttu-id="34c32-164">**장기적 절감**</span><span class="sxs-lookup"><span data-stu-id="34c32-164">**Long-term savings**</span></span> | <span data-ttu-id="34c32-165">처음 3년에 해당하는 SQL Server 라이선스를 구매하거나 갱신하는 것이 평균적으로 *연간 30% 더 저렴*합니다.</span><span class="sxs-lookup"><span data-stu-id="34c32-165">On average, it is *30% cheaper per year* to buy or renew a SQL Server license for the first 3 years.</span></span> <span data-ttu-id="34c32-166">또한 3년 후에 더 이상 라이선스를 갱신할 필요가 없고 Software Assurance 요금만 지급하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="34c32-166">Furthermore, after 3 years, you don’t need to renew the license anymore, just pay for Software Assurance.</span></span> <span data-ttu-id="34c32-167">이 시점에는 *200% 더 저렴*합니다.</span><span class="sxs-lookup"><span data-stu-id="34c32-167">At that point, it is *200% cheaper*.</span></span> |
| <span data-ttu-id="34c32-168">**무료 수동 보조 복제본**</span><span class="sxs-lookup"><span data-stu-id="34c32-168">**Free passive secondary replica**</span></span> | <span data-ttu-id="34c32-169">사용자 라이선스 필요의 또 다른 이점은 고가용성을 위해 SQL Server당 [하나의 수동 보조 복제본에 무료 라이선스가 제공](https://azure.microsoft.com/pricing/licensing-faq/)된다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="34c32-169">Another benefit of bringing your own license is the [free licensing for one passive secondary replica](https://azure.microsoft.com/pricing/licensing-faq/) per SQL Server for high availability purposes.</span></span> <span data-ttu-id="34c32-170">이에 따라 가용성이 높은 SQL Server 배포(예: Always On 가용성 그룹 사용)의 라이선스 비용이 50% 절감됩니다.</span><span class="sxs-lookup"><span data-stu-id="34c32-170">This cuts in half the licensing cost of a highly available SQL Server deployment (e.g. using Always On Availability Groups).</span></span> <span data-ttu-id="34c32-171">수동 보조 복제본을 실행할 권한은 장애 조치(failover) 서버 Software Assurance 이점을 통해 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="34c32-171">The rights to run the passive secondary are provided through the Fail-Over Servers Software Assurance benefit.</span></span> |

<span data-ttu-id="34c32-172">이러한 사용자 라이선스 필요 이미지 중 하나를 사용하여 SQL Server 2016 Azure VM을 만들려면 접두사 "{BYOL}"이 추가된 VM을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="34c32-172">To create a SQL Server 2016 Azure VM with one of these bring-your-own-license images, see the VMs prefixed with "{BYOL}":</span></span>

- [<span data-ttu-id="34c32-173">SQL Server 2016 Enterprise Azure VM</span><span class="sxs-lookup"><span data-stu-id="34c32-173">SQL Server 2016 Enterprise Azure VM</span></span>](https://ms.portal.azure.com/#create/Microsoft.BYOLSQLServer2016SP1EnterpriseWindowsServer2016)
- [<span data-ttu-id="34c32-174">SQL Server 2016 Standard Azure VM</span><span class="sxs-lookup"><span data-stu-id="34c32-174">SQL Server 2016 Standard Azure VM</span></span>](https://ms.portal.azure.com/#create/Microsoft.BYOLSQLServer2016SP1StandardWindowsServer2016)

> [!NOTE]
> <span data-ttu-id="34c32-175">Azure에서 사용할 SQL Server 라이선스 수를 10일 이내에 알려주세요.</span><span class="sxs-lookup"><span data-stu-id="34c32-175">Please let us know within 10 days how many SQL Server licenses you’ll use in Azure.</span></span> <span data-ttu-id="34c32-176">이전 이미지의 링크에는 이 작업을 수행하는 방법에 대한 지침이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34c32-176">The links to the previous images have instructions on how to do this.</span></span>

## <a name="avoid-unecessary-costs"></a><span data-ttu-id="34c32-177">불필요한 비용 방지</span><span class="sxs-lookup"><span data-stu-id="34c32-177">Avoid unecessary costs</span></span>

<span data-ttu-id="34c32-178">연속적으로 실행되지 않는 작업을 사용 중이면 비활성화된 동안 가상 컴퓨터를 종료하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="34c32-178">If you are using any workloads that do not run continuously, consider shutting down the virtual machine during the inactive periods.</span></span> <span data-ttu-id="34c32-179">사용한 양만큼만 요금을 지급합니다.</span><span class="sxs-lookup"><span data-stu-id="34c32-179">You only pay for what you use.</span></span>

<span data-ttu-id="34c32-180">예를 들어 Azure VM에서 SQL Server를 사용해 보려는 경우에는 실수로 몇 주 동안 계속 실행함으로써 요금이 발생하는 것을 원하지 않을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="34c32-180">For example, if you are simply trying out SQL Server on an Azure VM, you would not want to incur charges by accidentally leaving it running for weeks.</span></span> <span data-ttu-id="34c32-181">한 가지 해결 방법은 [automatic shutdown feature](https://azure.microsoft.com/blog/announcing-auto-shutdown-for-vms-using-azure-resource-manager/)(자동 종료 기능)를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="34c32-181">One solution is to use the [automatic shutdown feature](https://azure.microsoft.com/blog/announcing-auto-shutdown-for-vms-using-azure-resource-manager/).</span></span>

![SQL VM 자동 종료](./media/virtual-machines-windows-sql-server-pricing-guidance/sql-vm-auto-shutdown.png)

<span data-ttu-id="34c32-183">자동 종료는 [Azure DevTest Labs](https://azure.microsoft.com/services/devtest-lab)에서 제공되는 광범위한 유사 기능 집합에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="34c32-183">Automatic shutdown is part of a larger set of similar features provided by [Azure DevTest Labs](https://azure.microsoft.com/services/devtest-lab).</span></span>

<span data-ttu-id="34c32-184">다른 워크플로의 경우 [Azure Automation](https://azure.microsoft.com/services/automation/) 등의 스크립팅 솔루션을 사용하여 Azure VM을 자동으로 종료하고 다시 시작하는 방법을 고려하세요.</span><span class="sxs-lookup"><span data-stu-id="34c32-184">For other workflows, consider automatically shutting down and restarting Azure VMs with a scripting solution,such as [Azure Automation](https://azure.microsoft.com/services/automation/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="34c32-185">요금 청구를 방지하려면 VM을 종료하고 할당 해제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34c32-185">Shutting down and deallocating your VM is the only way to avoid charges.</span></span> <span data-ttu-id="34c32-186">단순히 중지하거나 전원 옵션을 사용하여 VM을 종료하면 사용당 요금이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="34c32-186">Simply stopping or using power options to shut down the VM still incurs usage charges.</span></span>

## <a name="next-steps"></a><span data-ttu-id="34c32-187">다음 단계</span><span class="sxs-lookup"><span data-stu-id="34c32-187">Next steps</span></span>

<span data-ttu-id="34c32-188">Azure 가격 책정 지침에 대해서는 [Azure 청구 및 비용 관리를 사용하여 예상치 못한 비용 방지](../../../billing/billing-getting-started.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="34c32-188">For general Azure pricing guidance, see [Prevent unexpected costs with Azure billing and cost management](../../../billing/billing-getting-started.md).</span></span>

<span data-ttu-id="34c32-189">SQL Server를 포함하여 최신 Virtual Machines 가격 책정에 대해서는 [Azure VM 가격 페이지](https://azure.microsoft.com/pricing/details/virtual-machines/sql-server-standard)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="34c32-189">For the latest Virtual Machines pricing, including SQL Server, see the [Azure VM pricing page](https://azure.microsoft.com/pricing/details/virtual-machines/sql-server-standard).</span></span>

<span data-ttu-id="34c32-190">[Azure Virtual Machines의 SQL Server 개요](virtual-machines-windows-sql-server-iaas-overview.md)에서 다른 SQL Server 가상 컴퓨터 항목을 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="34c32-190">Review other SQL Server Virtual Machine topics at [SQL Server on Azure Virtual Machines Overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
