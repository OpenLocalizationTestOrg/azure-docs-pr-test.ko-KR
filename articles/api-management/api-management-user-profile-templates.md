---
title: "Azure API Management의 사용자 프로필 템플릿 | Microsoft Docs"
description: "Azure API Management의 개발자 포털에서 사용자 프로필 페이지의 콘텐츠를 사용자 지정하는 방법을 알아봅니다."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 2e3b73ef-d223-44fe-9280-c3af3fd4a030
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 9a11bd5800068a5725ab2f099043993bff0b28d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="user-profile-templates-in-azure-api-management"></a><span data-ttu-id="d2b0e-103">Azure API Management의 사용자 프로필 템플릿</span><span class="sxs-lookup"><span data-stu-id="d2b0e-103">User profile templates in Azure API Management</span></span>
<span data-ttu-id="d2b0e-104">Azure API Management는 해당 콘텐츠를 구성하는 템플릿 집합을 사용하여 개발자 포털 페이지의 콘텐츠를 사용자 지정하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="d2b0e-105">이러한 템플릿에서 [DotLiquid](http://dotliquidmarkup.org/) 구문 및 [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers) 및 제공된 지역화 [String 리소스](api-management-template-resources.md#strings), [Glyph 리소스](api-management-template-resources.md#glyphs) 및 [Page 컨트롤](api-management-page-controls.md)의 집합과 같은 선택한 편집기를 사용하여 필요에 따라 페이지 콘텐츠를 유연하게 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="d2b0e-106">이 섹션의 템플릿을 통해 개발자 포털의 사용자 프로필 페이지의 콘텐츠를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-106">The templates in this section allow you to customize the content of the User profile pages in the developer portal.</span></span>  
  
-   [<span data-ttu-id="d2b0e-107">프로필</span><span class="sxs-lookup"><span data-stu-id="d2b0e-107">Profile</span></span>](#Profile)  
  
-   [<span data-ttu-id="d2b0e-108">구독</span><span class="sxs-lookup"><span data-stu-id="d2b0e-108">Subscriptions</span></span>](#Subscriptions)  
  
-   [<span data-ttu-id="d2b0e-109">응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="d2b0e-109">Applications</span></span>](#Applications)  
  
-   [<span data-ttu-id="d2b0e-110">계정 정보 업데이트</span><span class="sxs-lookup"><span data-stu-id="d2b0e-110">Update account info</span></span>](#UpdateAccountInfo)  
  
> [!NOTE]
>  <span data-ttu-id="d2b0e-111">다음 문서에는 샘플 기본 템플릿이 포함되어 있지만 지속적인 향상으로 인해 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-111">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span></span> <span data-ttu-id="d2b0e-112">원하는 개별 템플릿으로 이동하여 개발자 포털에서 라이브 기본 템플릿을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-112">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span></span> <span data-ttu-id="d2b0e-113">템플릿 작업에 대한 자세한 내용은 [템플릿을 사용하여 API Management 개발자 포털을 사용자 지정하는 방법](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-113">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="d2b0e-114"><a name="Profile"></a>프로필</span><span class="sxs-lookup"><span data-stu-id="d2b0e-114"><a name="Profile"></a> Profile</span></span>  
 <span data-ttu-id="d2b0e-115">**프로필** 템플릿을 사용하여 개발자 포털에서 사용자 프로필 페이지의 사용자 프로필 섹션을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-115">The **profile** template allows you to customize the user profile section of the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="d2b0e-116">![사용자 프로필 페이지](./media/api-management-user-profile-templates/APIM-User-Profile-Page.png "APIM 사용자 프로필 페이지")</span><span class="sxs-lookup"><span data-stu-id="d2b0e-116">![User Profile Page](./media/api-management-user-profile-templates/APIM-User-Profile-Page.png "APIM User Profile Page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="d2b0e-117">기본 템플릿</span><span class="sxs-lookup"><span data-stu-id="d2b0e-117">Default template</span></span>  
  
```xml  
<div class="pull-right">  
  {% if canChangePassword == true %}  
  <a class="btn btn-default" id="ChangePassword" role="button" href="{{changePasswordUrl}}">{% localized "UserProfile|ButtonLabelChangePassword" %}</a>  
  {% endif %}  
  <a id="changeAccountInfo" href="{{changeNameOrEmailUrl}}" class="btn btn-default">  
    <span class="glyphicon glyphicon-user"></span>  
    <span>{% localized "UserProfile|ButtonLabelChangeAccountInfo" %}</span>  
  </a>  
</div>  
<h2>{% localized "SubscriptionStrings|PageTitleDeveloperProfile" %}</h2>  
<div class="container-fluid">  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="Email">{% localized "UserProfile|TextboxLabelEmail" %}</label>  
    </div>  
    <div class="col-sm-9" id="Email">{{email}}</div>  
  </div>  
  
  {% if isSystemUser != true %}  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="FirstName">{% localized "UserProfile|TextboxLabelEmailFirstName" %}</label>  
    </div>  
    <div class="col-sm-9" id="FirstName">{{FirstName}}</div>  
  </div>  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="LastName">{% localized "UserProfile|TextboxLabelEmailLastName" %}</label>  
    </div>  
    <div class="col-sm-9" id="LastName">{{LastName}}</div>  
  </div>  
  {% else %}  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="CompanyName">{% localized "UserProfile|TextboxLabelOrganizationName" %}</label>  
    </div>  
    <div class="col-sm-9" id="CompanyName">{{CompanyName}}</div>  
  </div>  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="AddresserEmail">{% localized "UserProfile|TextboxLabelNotificationsSenderEmail" %}</label>  
    </div>  
    <div class="col-sm-9" id="AddresserEmail">{{AddresserEmail}}</div>  
  </div>  
  {% endif %}  
  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="d2b0e-118">컨트롤</span><span class="sxs-lookup"><span data-stu-id="d2b0e-118">Controls</span></span>  
 <span data-ttu-id="d2b0e-119">이 템플릿은 [페이지 컨트롤](api-management-page-controls.md)을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-119">This template may not use any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="d2b0e-120">데이터 모델</span><span class="sxs-lookup"><span data-stu-id="d2b0e-120">Data model</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="d2b0e-121">[프로필](#Profile), [응용 프로그램](#Applications) 및 [구독](#Subscriptions) 템플릿은 동일한 데이터 모델을 공유하며 동일한 템플릿 데이터를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-121">The [Profile](#Profile), [Applications](#Applications), and [Subscriptions](#Subscriptions) templates share the same data model and receive the same template data.</span></span>  
  
|<span data-ttu-id="d2b0e-122">속성</span><span class="sxs-lookup"><span data-stu-id="d2b0e-122">Property</span></span>|<span data-ttu-id="d2b0e-123">형식</span><span class="sxs-lookup"><span data-stu-id="d2b0e-123">Type</span></span>|<span data-ttu-id="d2b0e-124">설명</span><span class="sxs-lookup"><span data-stu-id="d2b0e-124">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="d2b0e-125">firstname</span><span class="sxs-lookup"><span data-stu-id="d2b0e-125">firstName</span></span>|<span data-ttu-id="d2b0e-126">string</span><span class="sxs-lookup"><span data-stu-id="d2b0e-126">string</span></span>|<span data-ttu-id="d2b0e-127">현재 사용자의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-127">First name of the current user.</span></span>|  
|<span data-ttu-id="d2b0e-128">Lastname</span><span class="sxs-lookup"><span data-stu-id="d2b0e-128">lastName</span></span>|<span data-ttu-id="d2b0e-129">string</span><span class="sxs-lookup"><span data-stu-id="d2b0e-129">string</span></span>|<span data-ttu-id="d2b0e-130">현재 사용의 성입니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-130">Last name of the current user.</span></span>|  
|<span data-ttu-id="d2b0e-131">companyName</span><span class="sxs-lookup"><span data-stu-id="d2b0e-131">companyName</span></span>|<span data-ttu-id="d2b0e-132">string</span><span class="sxs-lookup"><span data-stu-id="d2b0e-132">string</span></span>|<span data-ttu-id="d2b0e-133">현재 사용의 회사 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-133">The company name of the current user.</span></span>|  
|<span data-ttu-id="d2b0e-134">addresserEmail</span><span class="sxs-lookup"><span data-stu-id="d2b0e-134">addresserEmail</span></span>|<span data-ttu-id="d2b0e-135">string</span><span class="sxs-lookup"><span data-stu-id="d2b0e-135">string</span></span>|<span data-ttu-id="d2b0e-136">현재 사용의 전자 메일 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-136">Email address of the current user.</span></span>|  
|<span data-ttu-id="d2b0e-137">developersUsageStatisticsLinkk</span><span class="sxs-lookup"><span data-stu-id="d2b0e-137">developersUsageStatisticsLinkk</span></span>|<span data-ttu-id="d2b0e-138">string</span><span class="sxs-lookup"><span data-stu-id="d2b0e-138">string</span></span>|<span data-ttu-id="d2b0e-139">현재 사용자에 대한 분석을 볼 상대적 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-139">Relative URL to view analytics for the current user.</span></span>|  
|<span data-ttu-id="d2b0e-140">구독</span><span class="sxs-lookup"><span data-stu-id="d2b0e-140">subscriptions</span></span>|<span data-ttu-id="d2b0e-141">[구독](api-management-template-data-model-reference.md#Subscription) 엔터티의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-141">Collection of [Subscription](api-management-template-data-model-reference.md#Subscription) entities.</span></span>|<span data-ttu-id="d2b0e-142">현재 사용자에 대한 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-142">The subscriptions for the current user.</span></span>|  
|<span data-ttu-id="d2b0e-143">응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="d2b0e-143">applications</span></span>|<span data-ttu-id="d2b0e-144">[응용 프로그램](api-management-template-data-model-reference.md#Application) 엔터티의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-144">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="d2b0e-145">현재 사용자의 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-145">The applications of the current user.</span></span>|  
|<span data-ttu-id="d2b0e-146">changePasswordUrl</span><span class="sxs-lookup"><span data-stu-id="d2b0e-146">changePasswordUrl</span></span>|<span data-ttu-id="d2b0e-147">string</span><span class="sxs-lookup"><span data-stu-id="d2b0e-147">string</span></span>|<span data-ttu-id="d2b0e-148">현재 사용자의 암호를 변경할 상대적 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-148">The relative URL to change the current user's password.</span></span>|  
|<span data-ttu-id="d2b0e-149">changeNameOrEmailUrl</span><span class="sxs-lookup"><span data-stu-id="d2b0e-149">changeNameOrEmailUrl</span></span>|<span data-ttu-id="d2b0e-150">string</span><span class="sxs-lookup"><span data-stu-id="d2b0e-150">string</span></span>|<span data-ttu-id="d2b0e-151">현재 사용자에 대한 이름 및 전자 메일을 변경할 상대적 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-151">The relative URL to change the name and email for the current user.</span></span>|  
|<span data-ttu-id="d2b0e-152">canChangePassword</span><span class="sxs-lookup"><span data-stu-id="d2b0e-152">canChangePassword</span></span>|<span data-ttu-id="d2b0e-153">부울</span><span class="sxs-lookup"><span data-stu-id="d2b0e-153">boolean</span></span>|<span data-ttu-id="d2b0e-154">현재 사용자가 암호를 변경할 수 있는지 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-154">Whether the current user can change their password.</span></span>|  
|<span data-ttu-id="d2b0e-155">isSystemUser</span><span class="sxs-lookup"><span data-stu-id="d2b0e-155">isSystemUser</span></span>|<span data-ttu-id="d2b0e-156">부울</span><span class="sxs-lookup"><span data-stu-id="d2b0e-156">boolean</span></span>|<span data-ttu-id="d2b0e-157">현재 사용자가 기본 제공 [그룹](api-management-key-concepts.md#groups)의 구성원인지 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-157">Whether the current user is a member of one of the built-in [groups](api-management-key-concepts.md#groups).</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="d2b0e-158">샘플 템플릿 데이터</span><span class="sxs-lookup"><span data-stu-id="d2b0e-158">Sample template data</span></span>  
  
```json  
{  
    "firstName": "Administrator",  
    "lastName": "",  
    "companyName": "Contoso",  
    "addresserEmail": "apimgmt-noreply@mail.windowsazure.com",  
    "email": "admin@live.com",  
    "developersUsageStatisticsLink": "/Developer/Analytics",  
    "subscriptions": [  
        {  
            "Id": "57026e30de15d80041070001",  
            "ProductId": "57026e30de15d80041060001",  
            "ProductTitle": "Starter",  
            "ProductDescription": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060001",  
            "State": "Active",  
            "DisplayName": "Starter  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.847",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "b6b2870953d04420a4e02c58f2c08e74",  
            "SecondaryKey": "cfe28d5a1cd04d8abc93f48352076ea5",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070001/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070001/Renew"  
        },  
        {  
            "Id": "57026e30de15d80041070002",  
            "ProductId": "57026e30de15d80041060002",  
            "ProductTitle": "Unlimited",  
            "ProductDescription": "Subscribers have completely unlimited access to the API. Administrator approval is required.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060002",  
            "State": "Active",  
            "DisplayName": "Unlimited  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.923",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "8fe7843c36de4cceb4728e6cae297336",  
            "SecondaryKey": "96c850d217e74acf9b514ff8a5b38551",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070002/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070002/Renew"  
        }  
    ],  
    "applications": [],  
    "changePasswordUrl": "/account/password/change",  
    "changeNameOrEmailUrl": "/account/update",  
    "canChangePassword": false,  
    "isSystemUser": true  
}  
```  
  
##  <span data-ttu-id="d2b0e-159"><a name="Subscriptions"></a> 구독</span><span class="sxs-lookup"><span data-stu-id="d2b0e-159"><a name="Subscriptions"></a> Subscriptions</span></span>  
 <span data-ttu-id="d2b0e-160">**구독** 템플릿을 사용하여 개발자 포털에서 사용자 프로필 페이지의 구독 섹션을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-160">The **Subscriptions** template allows you to customize the subscriptions section of the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="d2b0e-161">![사용자 구독 페이지](./media/api-management-user-profile-templates/APIM-User-Subscription-Page.png "APIM 사용자 구독 페이지")</span><span class="sxs-lookup"><span data-stu-id="d2b0e-161">![User Subscription Page](./media/api-management-user-profile-templates/APIM-User-Subscription-Page.png "APIM User Subscription Page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="d2b0e-162">기본 템플릿</span><span class="sxs-lookup"><span data-stu-id="d2b0e-162">Default template</span></span>  
  
```xml  
<div class="ap-account-subscriptions">  
  <a href="{{developersUsageStatisticsLink}}" id="UsageStatistics" class="btn btn-default pull-right">  
    <span class="glyphicon glyphicon-stats"></span>  
    <span>{% localized "SubscriptionListStrings|WebDevelopersUsageStatisticsLink" %}</span>  
  </a>  
  
  <h2>{% localized "SubscriptionListStrings|WebDevelopersYourSubscriptions" %}</h2>  
  
  <table class="table">  
    <thead>  
      <tr>  
        <th>Subscription details</th>  
        <th>Product</th>  
        <th>{% localized "SubscriptionListStrings|WebDevelopersSubscriptionTableStateHeader" %}</th>  
        <th>Action</th>  
      </tr>  
    </thead>  
    <tbody>  
      {% if subscriptions.size == 0 %}  
      <tr>  
        <td class="text-center" colspan="4">  
          {% localized "CommonResources|NoItemsToDisplay" %}  
        </td>  
      </tr>  
      {% else %}  
      {% for subscription in subscriptions %}  
      <tr id="{{subscription.id}}" {% if subscription.hasExpired %} class="expired" {% endif %}>  
        <td>  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|SubscriptionPropertyLabelName" %}</label>  
            <div class="col-lg-6">  
              {{ subscription.displayName }}  
            </div>  
            <div class="col-lg-2">  
              <a class="btn-link" href="/Subscriptions/{{subscription.id}}/Rename">Rename</a>  
            </div>  
            <div class="clearfix"></div>  
          </div>  
          {% if subscription.isAwaitingApproval %}  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|SubscriptionPropertyLabelRequestedDate" %}</label>  
            <div class="col-lg-6">  
              {{ subscription.createdDate | date:"MM/dd/yyyy" }}  
            </div>  
          </div>  
          {% else %}  
          {% if subscription.isRejected == false %}  
          {% if subscription.startDate %}  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|SubscriptionPropertyLabelStartedDate" %}</label>  
            <div class="col-lg-6">  
              {{ subscription.startDate | date:"MM/dd/yyyy" }}  
            </div>  
          </div>  
          {% endif %}  
  
          <!-- ko with: Developers.Account.Root.account.key('{{subscription.primaryKey}}', '{{subscription.id}}', true) -->  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|WebDevelopersPrimaryKey" %}</label>  
            <div class="col-lg-6">  
              <code data-bind="text: $data.displayKey()" id="primary_{{subscription.id}}"></code>  
            </div>  
            <div class="col-lg-2">  
              <!-- ko if: !requestInProgress() -->  
              <div class="nowrap">  
                <a href="#" class="btn-link" id="togglePrimary_{{subscription.id}}" data-bind="click: toggleKeyDisplay, text: toggleKeyLabel"></a>  
                |  
                <a href="#" class="btn-link" id="regeneratePrimary_{{subscription.id}}" data-bind="click: regenerateKey, text: regenerateKeyLabel"></a>  
              </div>  
              <!-- /ko -->  
              <!-- ko if: requestInProgress() -->  
              <div class="progress progress-striped active">  
                <div class="progress-bar" role="progressbar" aria-valuenow="100" aria-valuemin="0" aria-valuemax="100" style="width: 100%">  
                  <span class="sr-only"></span>  
                </div>  
              </div>  
              <!-- /ko -->  
            </div>  
            <div class="clearfix"></div>  
          </div>  
          <!-- /ko -->  
          <!-- ko with: Developers.Account.Root.account.key('{{subscription.secondaryKey}}', '{{subscription.id}}', false) -->  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|WebDevelopersSecondaryKey" %}</label>  
            <div class="col-lg-6">  
              <code data-bind="text: $data.displayKey()" id="secondary_{{subscription.id}}"></code>  
            </div>  
            <div class="col-lg-2">  
              <div class="nowrap">  
                <a href="#" class="btn-link" id="toggleSecondary_{{subscription.id}}" data-bind="click: toggleKeyDisplay, text: toggleKeyLabel">{% localized "SubscriptionListStrings|ButtonLabelShowKey" %}</a>  
                |  
                <a href="#" class="btn-link" id="regenerateSecondary_{{subscription.id}}" data-bind="click: regenerateKey, text: regenerateKeyLabel">{% localized "SubscriptionListStrings|WebDevelopersRegenerateLink" %}</a>  
              </div>  
            </div>  
            <div class="clearfix"> </div>  
          </div>  
          <!-- /ko -->  
          {% endif %}  
          {% endif %}  
        </td>  
        <td>  
          <a href="{{subscription.productDetailsUrl}}">{{subscription.productTitle}}</a>  
        </td>  
        <td>  
          <strong>  
            {{subscription.state}}  
          </strong>  
        </td>  
        <td>  
          <div class="nowrap">  
            {% if subscription.canBeCancelled %}  
            <subscription-cancel params="{ subscriptionId: '{{subscription.id}}', cancelUrl: '{{subscription.cancelUrl}}' }"></subscription-cancel>  
            {% endif %}  
          </div>  
        </td>  
      </tr>  
      {% endfor %}  
      {% endif %}  
    </tbody>  
  </table>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="d2b0e-163">컨트롤</span><span class="sxs-lookup"><span data-stu-id="d2b0e-163">Controls</span></span>  
 <span data-ttu-id="d2b0e-164">이 템플릿에서 다음 [페이지 컨트롤](api-management-page-controls.md)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-164">This template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="d2b0e-165">subscription-cancel</span><span class="sxs-lookup"><span data-stu-id="d2b0e-165">subscription-cancel</span></span>](api-management-page-controls.md#subscription-cancel)  
  
### <a name="data-model"></a><span data-ttu-id="d2b0e-166">데이터 모델</span><span class="sxs-lookup"><span data-stu-id="d2b0e-166">Data model</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="d2b0e-167">[프로필](#Profile), [응용 프로그램](#Applications) 및 [구독](#Subscriptions) 템플릿은 동일한 데이터 모델을 공유하며 동일한 템플릿 데이터를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-167">The [Profile](#Profile), [Applications](#Applications), and [Subscriptions](#Subscriptions) templates share the same data model and receive the same template data.</span></span>  
  
|<span data-ttu-id="d2b0e-168">속성</span><span class="sxs-lookup"><span data-stu-id="d2b0e-168">Property</span></span>|<span data-ttu-id="d2b0e-169">형식</span><span class="sxs-lookup"><span data-stu-id="d2b0e-169">Type</span></span>|<span data-ttu-id="d2b0e-170">설명</span><span class="sxs-lookup"><span data-stu-id="d2b0e-170">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="d2b0e-171">firstname</span><span class="sxs-lookup"><span data-stu-id="d2b0e-171">firstName</span></span>|<span data-ttu-id="d2b0e-172">string</span><span class="sxs-lookup"><span data-stu-id="d2b0e-172">string</span></span>|<span data-ttu-id="d2b0e-173">현재 사용자의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-173">First name of the current user.</span></span>|  
|<span data-ttu-id="d2b0e-174">Lastname</span><span class="sxs-lookup"><span data-stu-id="d2b0e-174">lastName</span></span>|<span data-ttu-id="d2b0e-175">string</span><span class="sxs-lookup"><span data-stu-id="d2b0e-175">string</span></span>|<span data-ttu-id="d2b0e-176">현재 사용의 성입니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-176">Last name of the current user.</span></span>|  
|<span data-ttu-id="d2b0e-177">companyName</span><span class="sxs-lookup"><span data-stu-id="d2b0e-177">companyName</span></span>|<span data-ttu-id="d2b0e-178">string</span><span class="sxs-lookup"><span data-stu-id="d2b0e-178">string</span></span>|<span data-ttu-id="d2b0e-179">현재 사용의 회사 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-179">The company name of the current user.</span></span>|  
|<span data-ttu-id="d2b0e-180">addresserEmail</span><span class="sxs-lookup"><span data-stu-id="d2b0e-180">addresserEmail</span></span>|<span data-ttu-id="d2b0e-181">string</span><span class="sxs-lookup"><span data-stu-id="d2b0e-181">string</span></span>|<span data-ttu-id="d2b0e-182">현재 사용의 전자 메일 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-182">Email address of the current user.</span></span>|  
|<span data-ttu-id="d2b0e-183">developersUsageStatisticsLinkk</span><span class="sxs-lookup"><span data-stu-id="d2b0e-183">developersUsageStatisticsLinkk</span></span>|<span data-ttu-id="d2b0e-184">string</span><span class="sxs-lookup"><span data-stu-id="d2b0e-184">string</span></span>|<span data-ttu-id="d2b0e-185">현재 사용자에 대한 분석을 볼 상대적 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-185">Relative URL to view analytics for the current user.</span></span>|  
|<span data-ttu-id="d2b0e-186">구독</span><span class="sxs-lookup"><span data-stu-id="d2b0e-186">subscriptions</span></span>|<span data-ttu-id="d2b0e-187">[구독](api-management-template-data-model-reference.md#Subscription) 엔터티의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-187">Collection of [Subscription](api-management-template-data-model-reference.md#Subscription) entities.</span></span>|<span data-ttu-id="d2b0e-188">현재 사용자에 대한 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-188">The subscriptions for the current user.</span></span>|  
|<span data-ttu-id="d2b0e-189">응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="d2b0e-189">applications</span></span>|<span data-ttu-id="d2b0e-190">[응용 프로그램](api-management-template-data-model-reference.md#Application) 엔터티의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-190">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="d2b0e-191">현재 사용자의 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-191">The applications of the current user.</span></span>|  
|<span data-ttu-id="d2b0e-192">changePasswordUrl</span><span class="sxs-lookup"><span data-stu-id="d2b0e-192">changePasswordUrl</span></span>|<span data-ttu-id="d2b0e-193">string</span><span class="sxs-lookup"><span data-stu-id="d2b0e-193">string</span></span>|<span data-ttu-id="d2b0e-194">현재 사용자의 암호를 변경할 상대적 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-194">The relative URL to change the current user's password.</span></span>|  
|<span data-ttu-id="d2b0e-195">changeNameOrEmailUrl</span><span class="sxs-lookup"><span data-stu-id="d2b0e-195">changeNameOrEmailUrl</span></span>|<span data-ttu-id="d2b0e-196">string</span><span class="sxs-lookup"><span data-stu-id="d2b0e-196">string</span></span>|<span data-ttu-id="d2b0e-197">현재 사용자에 대한 이름 및 전자 메일을 변경할 상대적 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-197">The relative URL to change the name and email for the current user.</span></span>|  
|<span data-ttu-id="d2b0e-198">canChangePassword</span><span class="sxs-lookup"><span data-stu-id="d2b0e-198">canChangePassword</span></span>|<span data-ttu-id="d2b0e-199">부울</span><span class="sxs-lookup"><span data-stu-id="d2b0e-199">boolean</span></span>|<span data-ttu-id="d2b0e-200">현재 사용자가 암호를 변경할 수 있는지 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-200">Whether the current user can change their password.</span></span>|  
|<span data-ttu-id="d2b0e-201">isSystemUser</span><span class="sxs-lookup"><span data-stu-id="d2b0e-201">isSystemUser</span></span>|<span data-ttu-id="d2b0e-202">부울</span><span class="sxs-lookup"><span data-stu-id="d2b0e-202">boolean</span></span>|<span data-ttu-id="d2b0e-203">현재 사용자가 기본 제공 [그룹](api-management-key-concepts.md#groups)의 구성원인지 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-203">Whether the current user is a member of one of the built-in [groups](api-management-key-concepts.md#groups).</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="d2b0e-204">샘플 템플릿 데이터</span><span class="sxs-lookup"><span data-stu-id="d2b0e-204">Sample template data</span></span>  
  
```json  
{  
    "firstName": "Administrator",  
    "lastName": "",  
    "companyName": "Contoso",  
    "addresserEmail": "apimgmt-noreply@mail.windowsazure.com",  
    "email": "admin@live.com",  
    "developersUsageStatisticsLink": "/Developer/Analytics",  
    "subscriptions": [  
        {  
            "Id": "57026e30de15d80041070001",  
            "ProductId": "57026e30de15d80041060001",  
            "ProductTitle": "Starter",  
            "ProductDescription": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060001",  
            "State": "Active",  
            "DisplayName": "Starter  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.847",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "b6b2870953d04420a4e02c58f2c08e74",  
            "SecondaryKey": "cfe28d5a1cd04d8abc93f48352076ea5",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070001/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070001/Renew"  
        },  
        {  
            "Id": "57026e30de15d80041070002",  
            "ProductId": "57026e30de15d80041060002",  
            "ProductTitle": "Unlimited",  
            "ProductDescription": "Subscribers have completely unlimited access to the API. Administrator approval is required.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060002",  
            "State": "Active",  
            "DisplayName": "Unlimited  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.923",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "8fe7843c36de4cceb4728e6cae297336",  
            "SecondaryKey": "96c850d217e74acf9b514ff8a5b38551",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070002/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070002/Renew"  
        }  
    ],  
    "applications": [],  
    "changePasswordUrl": "/account/password/change",  
    "changeNameOrEmailUrl": "/account/update",  
    "canChangePassword": false,  
    "isSystemUser": true  
}  
```  
  
##  <span data-ttu-id="d2b0e-205"><a name="Applications"></a> 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="d2b0e-205"><a name="Applications"></a> Applications</span></span>  
 <span data-ttu-id="d2b0e-206">**응용 프로그램** 템플릿을 사용하여 개발자 포털에서 사용자 프로필 페이지의 구독 섹션을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-206">The **Applications** template allows you to customize the subscriptions section of the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="d2b0e-207">![사용자 계정 응용 프로그램 페이지](./media/api-management-user-profile-templates/APIM-User-Account-Applications-Page.png "APIM 사용자 계정 응용 프로그램 페이지")</span><span class="sxs-lookup"><span data-stu-id="d2b0e-207">![User Account Applications Page](./media/api-management-user-profile-templates/APIM-User-Account-Applications-Page.png "APIM User Account Applications Page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="d2b0e-208">기본 템플릿</span><span class="sxs-lookup"><span data-stu-id="d2b0e-208">Default template</span></span>  
  
```xml  
<div class="ap-account-applications">  
  <a id="RegisterApplication" href="/Developer/Applications/Register" class="btn btn-success pull-right">  
    <span class="glyphicon glyphicon-plus"></span>  
    <span>{% localized "ApplicationListStrings|WebDevelopersRegisterAppLink" %}</span>  
  </a>  
  <h2>{% localized "ApplicationListStrings|WebDevelopersYourApplicationsHeader" %}</h2>  
  
  <table class="table">  
    <thead>  
      <tr>  
        <th class="col-md-8">{% localized "ApplicationListStrings|WebDevelopersAppTableNameHeader" %}</th>  
        <th class="col-md-2">{% localized "ApplicationListStrings|WebDevelopersAppTableCategoryHeader" %}</th>  
        <th class="col-md-2" colspan="2">{% localized "ApplicationListStrings|WebDevelopersAppTableStateHeader" %}</th>  
      </tr>  
    </thead>  
    <tbody>  
  
      {% if applications.size == 0 %}  
  
      <tr>  
        <td class="col-md-12 text-center" colspan="4">  
          {% localized "CommonResources|NoItemsToDisplay" %}  
        </td>  
      </tr>  
  
      {% else %}  
  
      {% for app in applications %}  
      <tr>  
        <td class="col-md-8">  
          {{app.title}}  
        </td>  
        <td class="col-md-2">  
          {{app.categoryName}}  
        </td>  
        <td class="col-md-2">  
          <strong>  
            {% case app.state %}  
            {% when ApplicationStateModel.Registered %}  
            {% localized "ApplicationListStrings|WebDevelopersAppNotSubminted" %}  
  
            {% when ApplicationStateModel.Unpublished %}  
            {% localized "ApplicationListStrings|WebDevelopersAppNotPublished" %}  
  
            {% else %}  
            {{ app.state }}  
            {% endcase %}  
          </strong>  
        </td>  
        <td class="col-md-1">  
          <div class="nowrap">  
            {% if app.state != ApplicationStateModel.Submitted and app.state != ApplicationStateModel.Published %}  
            <app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
            {% endif %}  
          </div>  
        </td>  
      </tr>  
      {% endfor %}  
  
      {% endif %}  
    </tbody>  
  </table>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="d2b0e-209">컨트롤</span><span class="sxs-lookup"><span data-stu-id="d2b0e-209">Controls</span></span>  
 <span data-ttu-id="d2b0e-210">이 템플릿에서 다음 [페이지 컨트롤](api-management-page-controls.md)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-210">This template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="d2b0e-211">app-actions</span><span class="sxs-lookup"><span data-stu-id="d2b0e-211">app-actions</span></span>](api-management-page-controls.md#app-actions)  
  
### <a name="data-model"></a><span data-ttu-id="d2b0e-212">데이터 모델</span><span class="sxs-lookup"><span data-stu-id="d2b0e-212">Data model</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="d2b0e-213">[프로필](#Profile), [응용 프로그램](#Applications) 및 [구독](#Subscriptions) 템플릿은 동일한 데이터 모델을 공유하며 동일한 템플릿 데이터를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-213">The [Profile](#Profile), [Applications](#Applications), and [Subscriptions](#Subscriptions) templates share the same data model and receive the same template data.</span></span>  
  
|<span data-ttu-id="d2b0e-214">속성</span><span class="sxs-lookup"><span data-stu-id="d2b0e-214">Property</span></span>|<span data-ttu-id="d2b0e-215">형식</span><span class="sxs-lookup"><span data-stu-id="d2b0e-215">Type</span></span>|<span data-ttu-id="d2b0e-216">설명</span><span class="sxs-lookup"><span data-stu-id="d2b0e-216">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="d2b0e-217">firstname</span><span class="sxs-lookup"><span data-stu-id="d2b0e-217">firstName</span></span>|<span data-ttu-id="d2b0e-218">string</span><span class="sxs-lookup"><span data-stu-id="d2b0e-218">string</span></span>|<span data-ttu-id="d2b0e-219">현재 사용자의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-219">First name of the current user.</span></span>|  
|<span data-ttu-id="d2b0e-220">Lastname</span><span class="sxs-lookup"><span data-stu-id="d2b0e-220">lastName</span></span>|<span data-ttu-id="d2b0e-221">string</span><span class="sxs-lookup"><span data-stu-id="d2b0e-221">string</span></span>|<span data-ttu-id="d2b0e-222">현재 사용의 성입니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-222">Last name of the current user.</span></span>|  
|<span data-ttu-id="d2b0e-223">companyName</span><span class="sxs-lookup"><span data-stu-id="d2b0e-223">companyName</span></span>|<span data-ttu-id="d2b0e-224">string</span><span class="sxs-lookup"><span data-stu-id="d2b0e-224">string</span></span>|<span data-ttu-id="d2b0e-225">현재 사용의 회사 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-225">The company name of the current user.</span></span>|  
|<span data-ttu-id="d2b0e-226">addresserEmail</span><span class="sxs-lookup"><span data-stu-id="d2b0e-226">addresserEmail</span></span>|<span data-ttu-id="d2b0e-227">string</span><span class="sxs-lookup"><span data-stu-id="d2b0e-227">string</span></span>|<span data-ttu-id="d2b0e-228">현재 사용의 전자 메일 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-228">Email address of the current user.</span></span>|  
|<span data-ttu-id="d2b0e-229">developersUsageStatisticsLinkk</span><span class="sxs-lookup"><span data-stu-id="d2b0e-229">developersUsageStatisticsLinkk</span></span>|<span data-ttu-id="d2b0e-230">string</span><span class="sxs-lookup"><span data-stu-id="d2b0e-230">string</span></span>|<span data-ttu-id="d2b0e-231">현재 사용자에 대한 분석을 볼 상대적 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-231">Relative URL to view analytics for the current user.</span></span>|  
|<span data-ttu-id="d2b0e-232">구독</span><span class="sxs-lookup"><span data-stu-id="d2b0e-232">subscriptions</span></span>|<span data-ttu-id="d2b0e-233">[구독](api-management-template-data-model-reference.md#Subscription) 엔터티의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-233">Collection of [Subscription](api-management-template-data-model-reference.md#Subscription) entities.</span></span>|<span data-ttu-id="d2b0e-234">현재 사용자에 대한 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-234">The subscriptions for the current user.</span></span>|  
|<span data-ttu-id="d2b0e-235">응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="d2b0e-235">applications</span></span>|<span data-ttu-id="d2b0e-236">[응용 프로그램](api-management-template-data-model-reference.md#Application) 엔터티의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-236">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="d2b0e-237">현재 사용자의 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-237">The applications of the current user.</span></span>|  
|<span data-ttu-id="d2b0e-238">changePasswordUrl</span><span class="sxs-lookup"><span data-stu-id="d2b0e-238">changePasswordUrl</span></span>|<span data-ttu-id="d2b0e-239">string</span><span class="sxs-lookup"><span data-stu-id="d2b0e-239">string</span></span>|<span data-ttu-id="d2b0e-240">현재 사용자의 암호를 변경할 상대적 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-240">The relative URL to change the current user's password.</span></span>|  
|<span data-ttu-id="d2b0e-241">changeNameOrEmailUrl</span><span class="sxs-lookup"><span data-stu-id="d2b0e-241">changeNameOrEmailUrl</span></span>|<span data-ttu-id="d2b0e-242">string</span><span class="sxs-lookup"><span data-stu-id="d2b0e-242">string</span></span>|<span data-ttu-id="d2b0e-243">현재 사용자에 대한 이름 및 전자 메일을 변경할 상대적 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-243">The relative URL to change the name and email for the current user.</span></span>|  
|<span data-ttu-id="d2b0e-244">canChangePassword</span><span class="sxs-lookup"><span data-stu-id="d2b0e-244">canChangePassword</span></span>|<span data-ttu-id="d2b0e-245">부울</span><span class="sxs-lookup"><span data-stu-id="d2b0e-245">boolean</span></span>|<span data-ttu-id="d2b0e-246">현재 사용자가 암호를 변경할 수 있는지 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-246">Whether the current user can change their password.</span></span>|  
|<span data-ttu-id="d2b0e-247">isSystemUser</span><span class="sxs-lookup"><span data-stu-id="d2b0e-247">isSystemUser</span></span>|<span data-ttu-id="d2b0e-248">부울</span><span class="sxs-lookup"><span data-stu-id="d2b0e-248">boolean</span></span>|<span data-ttu-id="d2b0e-249">현재 사용자가 기본 제공 [그룹](api-management-key-concepts.md#groups)의 구성원인지 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-249">Whether the current user is a member of one of the built-in [groups](api-management-key-concepts.md#groups).</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="d2b0e-250">샘플 템플릿 데이터</span><span class="sxs-lookup"><span data-stu-id="d2b0e-250">Sample template data</span></span>  
  
```json  
{  
    "firstName": "Administrator",  
    "lastName": "",  
    "companyName": "Contoso",  
    "addresserEmail": "apimgmt-noreply@mail.windowsazure.com",  
    "email": "admin@live.com",  
    "developersUsageStatisticsLink": "/Developer/Analytics",  
    "subscriptions": [  
        {  
            "Id": "57026e30de15d80041070001",  
            "ProductId": "57026e30de15d80041060001",  
            "ProductTitle": "Starter",  
            "ProductDescription": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060001",  
            "State": "Active",  
            "DisplayName": "Starter  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.847",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "b6b2870953d04420a4e02c58f2c08e74",  
            "SecondaryKey": "cfe28d5a1cd04d8abc93f48352076ea5",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070001/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070001/Renew"  
        },  
        {  
            "Id": "57026e30de15d80041070002",  
            "ProductId": "57026e30de15d80041060002",  
            "ProductTitle": "Unlimited",  
            "ProductDescription": "Subscribers have completely unlimited access to the API. Administrator approval is required.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060002",  
            "State": "Active",  
            "DisplayName": "Unlimited  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.923",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "8fe7843c36de4cceb4728e6cae297336",  
            "SecondaryKey": "96c850d217e74acf9b514ff8a5b38551",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070002/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070002/Renew"  
        }  
    ],  
    "applications": [],  
    "changePasswordUrl": "/account/password/change",  
    "changeNameOrEmailUrl": "/account/update",  
    "canChangePassword": false,  
    "isSystemUser": true  
}  
```  
  
##  <span data-ttu-id="d2b0e-251"><a name="UpdateAccountInfo"></a> 계정 정보 업데이트</span><span class="sxs-lookup"><span data-stu-id="d2b0e-251"><a name="UpdateAccountInfo"></a> Update account info</span></span>  
 <span data-ttu-id="d2b0e-252">**계정 정보 업데이트** 템플릿을 사용하여 개발자 포털의 **계정 정보 업데이트** 페이지를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-252">The **Uodate account info** template allows you to customize the **Update account information** page in the developer portal.</span></span>  
  
 <span data-ttu-id="d2b0e-253">![사용자 계정 정보 페이지 개발자 포털 템플릿](./media/api-management-user-profile-templates/APIM-User-Account-Info-Page-Developer-Portal-Templates.png "APIM 사용자 계정 정보 페이지 개발자 포털 템플릿")</span><span class="sxs-lookup"><span data-stu-id="d2b0e-253">![User Account Info Page Developer Portal Templates](./media/api-management-user-profile-templates/APIM-User-Account-Info-Page-Developer-Portal-Templates.png "APIM User Account Info Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="d2b0e-254">기본 템플릿</span><span class="sxs-lookup"><span data-stu-id="d2b0e-254">Default template</span></span>  
  
```xml  
<div class="row">  
  <div class="col-sm-6 col-md-6">  
    <div class="form-group">  
      <label for="Email">{% localized "SigninResources|TextboxLabelEmail" %}</label>  
      <input autofocus="autofocus" class="form-control" id="Email" name="Email" type="text" value="{{email}}">  
    </div>  
    <div class="form-group">  
      <label for="FirstName">{% localized "SigninResources|TextboxLabelEmailFirstName" %}</label>  
      <input class="form-control" id="FirstName" name="FirstName" type="text" value="{{firstName}}">  
    </div>  
    <div class="form-group">  
      <label for="LastName">{% localized "SigninResources|TextboxLabelEmailLastName" %}</label>  
      <input class="form-control" id="LastName" name="LastName" type="text" value="{{lastName}}">  
    </div>  
    <div class="form-group">  
      <label for="Password">{% localized "SigninResources|WebAuthenticationSigninPasswordLabel" %}</label>  
      <input class="form-control" id="Password" name="Password" type="password">  
    </div>  
  </div>  
</div>  
  
<button type="submit" class="btn btn-primary" id="UpdateProfile">  
  {% localized "UpdateProfileStrings|ButtonLabelUpdateProfile" %}  
</button>  
<a class="btn btn-default" href="/developer" role="button">  
  {% localized "CommonStrings|ButtonLabelCancel" %}  
</a>  
```  
  
### <a name="controls"></a><span data-ttu-id="d2b0e-255">컨트롤</span><span class="sxs-lookup"><span data-stu-id="d2b0e-255">Controls</span></span>  
 <span data-ttu-id="d2b0e-256">이 템플릿은 [페이지 컨트롤](api-management-page-controls.md)을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-256">This template may not use any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="d2b0e-257">데이터 모델</span><span class="sxs-lookup"><span data-stu-id="d2b0e-257">Data model</span></span>  
 <span data-ttu-id="d2b0e-258">[사용자 계정 정보](api-management-template-data-model-reference.md#UserAccountInfo) 엔터티입니다.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-258">[User account info](api-management-template-data-model-reference.md#UserAccountInfo) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="d2b0e-259">샘플 템플릿 데이터</span><span class="sxs-lookup"><span data-stu-id="d2b0e-259">Sample template data</span></span>  
  
```json  
{  
    "FirstName": "Administrator",  
    "LastName": "",  
    "Email": "admin@live.com",  
    "Password": null,  
    "NameIdentifier": null,  
    "ProviderName": null,  
    "IsBasicAccount": false  
}  
```

## <a name="next-steps"></a><span data-ttu-id="d2b0e-260">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d2b0e-260">Next steps</span></span>
<span data-ttu-id="d2b0e-261">템플릿 작업에 대한 자세한 내용은 [템플릿을 사용하여 API Management 개발자 포털을 사용자 지정하는 방법](api-management-developer-portal-templates.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-261">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>