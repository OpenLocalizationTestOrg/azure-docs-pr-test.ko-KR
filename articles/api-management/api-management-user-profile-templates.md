---
title: "aaa \"Azure API 관리에서 사용자 프로필 템플릿 | \"Microsoft Docs"
description: "Azure API 관리에서 hello 개발자 포털에서의 사용자 프로필 hello toocustomize hello 콘텐츠 페이지 방식에 대해 알아봅니다."
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
ms.openlocfilehash: c8f153b310221164809acf58e4af236928ceb41d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="user-profile-templates-in-azure-api-management"></a>Azure API Management의 사용자 프로필 템플릿
Azure API 관리 개발자 포털 페이지 콘텐츠를 구성 하는 템플릿 집합을 사용 하 여 콘텐츠의 toocustomize hello 기능 hello를 제공 합니다. 사용 하 여 [DotLiquid](http://dotliquidmarkup.org/) 구문 및 hello 편집기의 선택한와 같은 [디자이너에 대 한 DotLiquid](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), 제공 된 집합을 지역화 [문자열 리소스](api-management-template-resources.md#strings), [ 문자 모양 리소스](api-management-template-resources.md#glyphs), 및 [컨트롤 페이지](api-management-page-controls.md), 이러한 템플릿을 사용 하 여 나타나며 hello 페이지의 뛰어난 유연성 tooconfigure hello 내용을 백업이 있어야 합니다.  
  
 이 섹션의 hello 템플릿을 hello 개발자 포털에서 toocustomize hello 내용의 hello 사용자 프로필 페이지를 사용 합니다.  
  
-   [프로필](#Profile)  
  
-   [구독](#Subscriptions)  
  
-   [응용 프로그램](#Applications)  
  
-   [계정 정보 업데이트](#UpdateAccountInfo)  
  
> [!NOTE]
>  예제 기본 서식 파일 설명서, hello에 포함 되었지만 이러한 toocontinuous 개선 인해 주체 toochange 됩니다. 원하는 toohello 개별 서식 파일을 이동 하 여 hello 라이브 기본 템플릿 hello 개발자 포털에서 볼 수 있습니다. 서식 파일 사용에 대 한 자세한 내용은 참조 [어떻게 toocustomize hello 템플릿을 사용 하 여 API 관리 개발자 포털](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/)합니다.  
  
##  <a name="Profile"></a>프로필  
 hello **프로필** 템플릿을 사용 하 여 hello 개발자 포털에서 사용자 프로필 페이지 hello toocustomize hello 사용자 프로필 섹션.  
  
 ![사용자 프로필 페이지](./media/api-management-user-profile-templates/APIM-User-Profile-Page.png "APIM 사용자 프로필 페이지")  
  
### <a name="default-template"></a>기본 템플릿  
  
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
  
### <a name="controls"></a>컨트롤  
 이 템플릿은 [페이지 컨트롤](api-management-page-controls.md)을 사용할 수 없습니다.  
  
### <a name="data-model"></a>데이터 모델  
  
> [!NOTE]
>  hello [프로필](#Profile), [응용 프로그램](#Applications), 및 [구독](#Subscriptions) 템플릿은 동일한 데이터 모델 및 hello 수신 hello 공유 같은 템플릿 데이터입니다.  
  
|속성|형식|설명|  
|--------------|----------|-----------------|  
|firstname|string|Hello 현재 사용자의 이름입니다.|  
|Lastname|string|Hello 현재 사용자의 성입니다.|  
|companyName|string|hello hello 현재 사용자의 회사 이름입니다.|  
|addresserEmail|string|Hello 현재 사용자의 전자 메일 주소입니다.|  
|developersUsageStatisticsLinkk|string|Hello 현재 사용자에 대 한 상대 URL tooview 분석 합니다.|  
|구독|[구독](api-management-template-data-model-reference.md#Subscription) 엔터티의 컬렉션입니다.|hello 현재 사용자에 대 한 hello 구독 합니다.|  
|응용 프로그램|[응용 프로그램](api-management-template-data-model-reference.md#Application) 엔터티의 컬렉션입니다.|hello 현재 사용자의 hello 응용 프로그램입니다.|  
|changePasswordUrl|string|hello 상대 URL toochange hello 현재 사용자의 암호입니다.|  
|changeNameOrEmailUrl|string|상대 URL toochange hello 이름 및 전자 메일 hello 현재 사용자에 대 한 hello 합니다.|  
|canChangePassword|부울|여부 hello 현재 사용자가 암호를 변경할 수 있습니다.|  
|isSystemUser|부울|Hello 현재 사용자의 기본 제공 hello 중 하나의 멤버 인지 [그룹](api-management-key-concepts.md#groups)합니다.|  
  
### <a name="sample-template-data"></a>샘플 템플릿 데이터  
  
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
            "ProductDescription": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",  
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
            "ProductDescription": "Subscribers have completely unlimited access toohello API. Administrator approval is required.",  
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
  
##  <a name="Subscriptions"></a> 구독  
 hello **구독** 템플릿을 사용 하 여 hello 개발자 포털에서 hello 사용자 프로필 페이지 toocustomize hello 구독 섹션.  
  
 ![사용자 구독 페이지](./media/api-management-user-profile-templates/APIM-User-Subscription-Page.png "APIM 사용자 구독 페이지")  
  
### <a name="default-template"></a>기본 템플릿  
  
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
  
### <a name="controls"></a>컨트롤  
 이 템플릿은 hello 다음을 사용할 수 있습니다 [컨트롤 페이지](api-management-page-controls.md)합니다.  
  
-   [subscription-cancel](api-management-page-controls.md#subscription-cancel)  
  
### <a name="data-model"></a>데이터 모델  
  
> [!NOTE]
>  hello [프로필](#Profile), [응용 프로그램](#Applications), 및 [구독](#Subscriptions) 템플릿은 동일한 데이터 모델 및 hello 수신 hello 공유 같은 템플릿 데이터입니다.  
  
|속성|형식|설명|  
|--------------|----------|-----------------|  
|firstname|string|Hello 현재 사용자의 이름입니다.|  
|Lastname|string|Hello 현재 사용자의 성입니다.|  
|companyName|string|hello hello 현재 사용자의 회사 이름입니다.|  
|addresserEmail|string|Hello 현재 사용자의 전자 메일 주소입니다.|  
|developersUsageStatisticsLinkk|string|Hello 현재 사용자에 대 한 상대 URL tooview 분석 합니다.|  
|구독|[구독](api-management-template-data-model-reference.md#Subscription) 엔터티의 컬렉션입니다.|hello 현재 사용자에 대 한 hello 구독 합니다.|  
|응용 프로그램|[응용 프로그램](api-management-template-data-model-reference.md#Application) 엔터티의 컬렉션입니다.|hello 현재 사용자의 hello 응용 프로그램입니다.|  
|changePasswordUrl|string|hello 상대 URL toochange hello 현재 사용자의 암호입니다.|  
|changeNameOrEmailUrl|string|상대 URL toochange hello 이름 및 전자 메일 hello 현재 사용자에 대 한 hello 합니다.|  
|canChangePassword|부울|여부 hello 현재 사용자가 암호를 변경할 수 있습니다.|  
|isSystemUser|부울|Hello 현재 사용자의 기본 제공 hello 중 하나의 멤버 인지 [그룹](api-management-key-concepts.md#groups)합니다.|  
  
### <a name="sample-template-data"></a>샘플 템플릿 데이터  
  
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
            "ProductDescription": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",  
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
            "ProductDescription": "Subscribers have completely unlimited access toohello API. Administrator approval is required.",  
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
  
##  <a name="Applications"></a> 응용 프로그램  
 hello **응용 프로그램** 템플릿을 사용 하 여 hello 개발자 포털에서 hello 사용자 프로필 페이지 toocustomize hello 구독 섹션.  
  
 ![사용자 계정 응용 프로그램 페이지](./media/api-management-user-profile-templates/APIM-User-Account-Applications-Page.png "APIM 사용자 계정 응용 프로그램 페이지")  
  
### <a name="default-template"></a>기본 템플릿  
  
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
  
### <a name="controls"></a>컨트롤  
 이 템플릿은 hello 다음을 사용할 수 있습니다 [컨트롤 페이지](api-management-page-controls.md)합니다.  
  
-   [app-actions](api-management-page-controls.md#app-actions)  
  
### <a name="data-model"></a>데이터 모델  
  
> [!NOTE]
>  hello [프로필](#Profile), [응용 프로그램](#Applications), 및 [구독](#Subscriptions) 템플릿은 동일한 데이터 모델 및 hello 수신 hello 공유 같은 템플릿 데이터입니다.  
  
|속성|형식|설명|  
|--------------|----------|-----------------|  
|firstname|string|Hello 현재 사용자의 이름입니다.|  
|Lastname|string|Hello 현재 사용자의 성입니다.|  
|companyName|string|hello hello 현재 사용자의 회사 이름입니다.|  
|addresserEmail|string|Hello 현재 사용자의 전자 메일 주소입니다.|  
|developersUsageStatisticsLinkk|string|Hello 현재 사용자에 대 한 상대 URL tooview 분석 합니다.|  
|구독|[구독](api-management-template-data-model-reference.md#Subscription) 엔터티의 컬렉션입니다.|hello 현재 사용자에 대 한 hello 구독 합니다.|  
|응용 프로그램|[응용 프로그램](api-management-template-data-model-reference.md#Application) 엔터티의 컬렉션입니다.|hello 현재 사용자의 hello 응용 프로그램입니다.|  
|changePasswordUrl|string|hello 상대 URL toochange hello 현재 사용자의 암호입니다.|  
|changeNameOrEmailUrl|string|상대 URL toochange hello 이름 및 전자 메일 hello 현재 사용자에 대 한 hello 합니다.|  
|canChangePassword|부울|여부 hello 현재 사용자가 암호를 변경할 수 있습니다.|  
|isSystemUser|부울|Hello 현재 사용자의 기본 제공 hello 중 하나의 멤버 인지 [그룹](api-management-key-concepts.md#groups)합니다.|  
  
### <a name="sample-template-data"></a>샘플 템플릿 데이터  
  
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
            "ProductDescription": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",  
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
            "ProductDescription": "Subscribers have completely unlimited access toohello API. Administrator approval is required.",  
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
  
##  <a name="UpdateAccountInfo"></a> 계정 정보 업데이트  
 hello **Uodate 계정 정보** 템플릿을 사용 하 여 toocustomize hello **계정 정보를 업데이트** hello 개발자 포털에서 페이지입니다.  
  
 ![사용자 계정 정보 페이지 개발자 포털 템플릿](./media/api-management-user-profile-templates/APIM-User-Account-Info-Page-Developer-Portal-Templates.png "APIM 사용자 계정 정보 페이지 개발자 포털 템플릿")  
  
### <a name="default-template"></a>기본 템플릿  
  
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
  
### <a name="controls"></a>컨트롤  
 이 템플릿은 [페이지 컨트롤](api-management-page-controls.md)을 사용할 수 없습니다.  
  
### <a name="data-model"></a>데이터 모델  
 [사용자 계정 정보](api-management-template-data-model-reference.md#UserAccountInfo) 엔터티입니다.  
  
### <a name="sample-template-data"></a>샘플 템플릿 데이터  
  
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

## <a name="next-steps"></a>다음 단계
서식 파일 사용에 대 한 자세한 내용은 참조 [어떻게 toocustomize hello 템플릿을 사용 하 여 API 관리 개발자 포털](api-management-developer-portal-templates.md)합니다.
