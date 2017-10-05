---
title: "Azure 클래식 포털의 알려진 네트워크 | Microsoft Docs"
description: "알려진 네트워크를 구성하여 조직 소유의 IP 주소가 여러 지역에서의 로그인 및 의심스러운 활동을 포함하는 IP 주소의 로그인 보고서에 포함되지 않도록 할 수 있습니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: f56e042a-78d5-4ea3-be33-94004f2a0fc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: e4d51d1d2f09fca34d749879e21d49f785eac35c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="known-networks"></a><span data-ttu-id="bf740-103">알려진 네트워크</span><span class="sxs-lookup"><span data-stu-id="bf740-103">Known networks</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="bf740-104">Azure 클래식 포털</span><span class="sxs-lookup"><span data-stu-id="bf740-104">Azure classic portal</span></span>](active-directory-known-networks.md)
> * [<span data-ttu-id="bf740-105">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="bf740-105">Azure portal</span></span>](active-directory-known-networks-azure-portal.md)
> 
> 


<span data-ttu-id="bf740-106">Azure Active Directory의 액세스 및 사용 보고서를 사용하여 조직 디렉터리의 무결성 및 보안을 볼 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="bf740-106">You can use Azure Active Directory's access and usage reports to gain visibility into the integrity and security of your organization’s directory.</span></span> <span data-ttu-id="bf740-107">이 정보를 사용하면 디렉터리 관리자는 가능한 보안 위험이 발생할 수 있는 위치를 보다 잘 결정하여 이러한 위험을 적절하게 완화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf740-107">With this information, a directory admin can better determine where possible security risks may lie so that they can adequately plan to mitigate those risks.</span></span>

<span data-ttu-id="bf740-108">“*여러 지역에서의 로그인*” 및 “*의심스러운 활동을 포함하는 IP 주소의 로그인*” 보고서에 조직이 실제로 소유하는 IP 주소가 잘못 플래깅될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf740-108">It is possible that the “*Sign ins from multiple geographies*” and “*Sign ins from IP addresses with suspicious activity*” reports incorrectly flag IP addresses that are actually owned by your organization.</span></span> 

<span data-ttu-id="bf740-109">예를 들어 다음과 같은 경우에 이러한 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf740-109">This can, for example, happen when:</span></span> 

* <span data-ttu-id="bf740-110">Boston 사무실의 사용자가 San Francisco의 데이터 센터에 원격으로 로그인하여 "여러 지역에서의 로그인" 보고서 트리거</span><span class="sxs-lookup"><span data-stu-id="bf740-110">A user in your Boston office has signed in remotely to your data center in San Francisco triggers the “Sign ins from multiple geographies” report</span></span> 
* <span data-ttu-id="bf740-111">조직의 사용자가 잘못된 암호로 여러 번 로그온을 시도하여 “의심스러운 활동을 포함하는 IP 주소의 로그인” 보고서 트리거</span><span class="sxs-lookup"><span data-stu-id="bf740-111">A user of your organization tries to sign-on several times with an incorrect password triggers the “Sign ins from IP addresses with suspicious activity” report</span></span> 

<span data-ttu-id="bf740-112">이러한 문제로 인해 잘못된 보안 보고서가 생성되지 않도록 하려면 조직의 공용 IP 주소 목록에 알려진 IP 주소 범위를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf740-112">To prevent these cases from generating misleading security reports, you should add known IP address ranges to the list of your organization's public IP address.</span></span>    

### <a name="to-add-your-organizations-public-ip-address-ranges-perform-the-following-steps"></a><span data-ttu-id="bf740-113">조직의 공용 IP 주소 범위를 추가하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="bf740-113">To add your organization’s public IP address ranges, perform the following steps:</span></span>

1. <span data-ttu-id="bf740-114">[Azure 관리 포털](https://manage.windowsazure.com)에 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="bf740-114">Sign-on to the [Azure management portal](https://manage.windowsazure.com).</span></span>

2. <span data-ttu-id="bf740-115">왼쪽 창에서 **Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bf740-115">In the left pane, click **Active Directory**.</span></span> 

    ![알려진 네트워크](./media/active-directory-known-networks/known-netwoks-01.png)

3. <span data-ttu-id="bf740-117">**디렉터리** 탭에서 해당 디렉터리를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bf740-117">In the **Directory** tab, select your directory.</span></span>

4. <span data-ttu-id="bf740-118">위쪽 메뉴에서 **구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bf740-118">In the menu on the top, click **Configure**.</span></span> 

    ![알려진 네트워크](./media/active-directory-known-networks/known-netwoks-02.png)

5. <span data-ttu-id="bf740-120">구성 탭에서 **조직의 공용 IP 주소 범위**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="bf740-120">On the Configure tab, go to **your organizations public IP address ranges**</span></span> 

    ![알려진 네트워크](./media/active-directory-known-networks/known-netwoks-03.png)

6. <span data-ttu-id="bf740-122">**알려진 IP 주소 범위 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bf740-122">Click **Add Known IP Address Ranges**.</span></span>

7. <span data-ttu-id="bf740-123">나타나는 대화 상자에서 주소 범위를 추가하고 완료되면 확인 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="bf740-123">Add your address ranges in the dialog box that appears, and then click the check button  when you are done.</span></span> 

    ![알려진 네트워크](./media/active-directory-known-networks/known-netwoks-04.png)

<span data-ttu-id="bf740-125">**추가 리소스:**</span><span class="sxs-lookup"><span data-stu-id="bf740-125">**Additional resources:**</span></span>

* [<span data-ttu-id="bf740-126">액세스 및 사용 보고서 보기</span><span class="sxs-lookup"><span data-stu-id="bf740-126">View your access and usage reports</span></span>](active-directory-view-access-usage-reports.md)
* [<span data-ttu-id="bf740-127">의심스러운 활동을 포함하는 IP 주소의 로그인</span><span class="sxs-lookup"><span data-stu-id="bf740-127">Sign ins from IP addresses with suspicious activity</span></span>](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md)
* [<span data-ttu-id="bf740-128">여러 지역에서의 로그인</span><span class="sxs-lookup"><span data-stu-id="bf740-128">Sign ins from multiple geographies</span></span>](active-directory-reporting-sign-ins-from-multiple-geographies.md)

