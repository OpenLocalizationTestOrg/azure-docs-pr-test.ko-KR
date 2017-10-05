---
title: "Twilio에서 전화를 거는 방법(.NET) | Microsoft Docs"
description: "Azure에서 Twilio API 서비스를 사용하여 전화를 걸고 SMS 메시지를 보내는 방법에 대해 알아봅니다. 코드 샘플은 .NET으로 작성되었습니다."
services: 
documentationcenter: .net
author: devinrader
manager: timlt
editor: 
ms.assetid: 789185ad-69dc-4e9e-a936-42e0a25315c8
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/04/2016
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: 0899a49cbfda775017dab7fc6d8963bbeb86d74c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-make-a-phone-call-using-twilio-in-a-web-role-on-azure"></a><span data-ttu-id="f0205-104">Azure의 웹 역할에서 Twilio를 사용하여 전화를 거는 방법</span><span class="sxs-lookup"><span data-stu-id="f0205-104">How to make a phone call using Twilio in a web role on Azure</span></span>
<span data-ttu-id="f0205-105">이 가이드에서는 Azure에 호스트된 웹 페이지에서 Twilio를 사용하여 전화를 거는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f0205-105">This guide demonstrates how to use Twilio to make a call from a web page hosted in Azure.</span></span> <span data-ttu-id="f0205-106">결과적으로 응용 프로그램은 다음 스크린샷에 표시된 대로 지정된 번호와 메시지를 사용하여 호출하라는 메시지를 사용자에게 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="f0205-106">The resulting application prompts the user to make a call with the given number and message, as shown in the following screenshot.</span></span>

![Twilio 및 ASP.NET을 사용하는 Azure 통화 양식][twilio_dotnet_basic_form]

## <span data-ttu-id="f0205-108"><a name="twilio-prereqs"></a>필수 조건</span><span class="sxs-lookup"><span data-stu-id="f0205-108"><a name="twilio-prereqs"></a>Prerequisites</span></span>
<span data-ttu-id="f0205-109">이 항목에서 코드를 사용하려면 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0205-109">You will need to do the following to use the code in this topic:</span></span>

1. <span data-ttu-id="f0205-110">[Twilio 콘솔][twilio_console]에서 Twilio 계정 및 인증 토큰을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f0205-110">Acquire a Twilio account and authentication token from the [Twilio Console][twilio_console].</span></span> <span data-ttu-id="f0205-111">Twilio를 시작하려면 [https://www.twilio.com/try-twilio][try_twilio]에서 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="f0205-111">To get started with Twilio, sign up at [https://www.twilio.com/try-twilio][try_twilio].</span></span> <span data-ttu-id="f0205-112">[http://www.twilio.com/pricing][twilio_pricing]에서 가격을 평가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0205-112">You can evaluate pricing at [http://www.twilio.com/pricing][twilio_pricing].</span></span> <span data-ttu-id="f0205-113">Twilio에서 제공하는 API에 대한 내용은 [http://www.twilio.com/voice/api][twilio_api]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f0205-113">For information about the API provided by Twilio, see [http://www.twilio.com/voice/api][twilio_api].</span></span>
2. <span data-ttu-id="f0205-114">*Twilio .NET 라이브러리*를 웹 역할에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f0205-114">Add the *Twilio .NET libary* to your web role.</span></span> <span data-ttu-id="f0205-115">이 항목의 뒷부분에 나오는 **웹 역할 프로젝트에 Twilio 라이브러리를 추가하려면**을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f0205-115">See **To add the Twilio libraries to your web role project**, later in this topic.</span></span>

<span data-ttu-id="f0205-116">[Azure에서 기본적인 웹 역할][azure_webroles_get_started] 만들기에 익숙해져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0205-116">You should be familiar with creating a basic [Web Role on Azure][azure_webroles_get_started].</span></span>

## <span data-ttu-id="f0205-117"><a name="howtocreateform"></a>방법: 전화 걸기 웹 양식 만들기</span><span class="sxs-lookup"><span data-stu-id="f0205-117"><a name="howtocreateform"></a>How to: Create a web form for making a call</span></span>
<span data-ttu-id="f0205-118"><a id="use_nuget"></a>웹 역할 프로젝트에 Twilio 라이브러리 추가하려면</span><span class="sxs-lookup"><span data-stu-id="f0205-118"><a id="use_nuget"></a>To add the Twilio libraries to your web role project:</span></span>

1. <span data-ttu-id="f0205-119">Visual Studio에서 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f0205-119">Open your solution in Visual Studio.</span></span>
2. <span data-ttu-id="f0205-120">**참조**를 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f0205-120">Right-click **References**.</span></span>
3. <span data-ttu-id="f0205-121">**NuGet 패키지 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f0205-121">Click **Manage NuGet Packages**.</span></span>
4. <span data-ttu-id="f0205-122">**온라인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f0205-122">Click **Online**.</span></span>
5. <span data-ttu-id="f0205-123">온라인 검색 상자에 *twilio*를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f0205-123">In the search online box, type *twilio*.</span></span>
6. <span data-ttu-id="f0205-124">Twilio 패키지에서 **설치** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f0205-124">Click **Install** on the Twilio package.</span></span>

<span data-ttu-id="f0205-125">다음 코드는 전화를 걸기 위해 웹 양식을 만들고 사용자 데이터를 검색하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f0205-125">The following code shows how to create a web form to retrieve user data for making a call.</span></span> <span data-ttu-id="f0205-126">이 예제에서는 **TwilioCloud**라는 ASP.NET 웹 역할이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0205-126">In this example, an ASP.NET Web Role named **TwilioCloud** is created.</span></span>

```aspx
<%@ Page Title="Home Page" Language="C#" MasterPageFile="~/Site.master"
    AutoEventWireup="true" CodeBehind="Default.aspx.cs"
    Inherits="WebRole1._Default" %>

<asp:Content ID="HeaderContent" runat="server" ContentPlaceHolderID="HeadContent">
</asp:Content>
<asp:Content ID="BodyContent" runat="server" ContentPlaceHolderID="MainContent">
    <div>
        <asp:BulletedList ID="varDisplay" runat="server" BulletStyle="NotSet">
        </asp:BulletedList>
    </div>
    <div>
        <p>Fill in all fields and click <b>Make this call</b>.</p>
        <div>
            To:<br /><asp:TextBox ID="toNumber" runat="server" /><br /><br />
            Message:<br /><asp:TextBox ID="message" runat="server" /><br /><br />
            <asp:Button ID="callpage" runat="server" Text="Make this call"
                onclick="callpage_Click" />
        </div>
    </div>
</asp:Content>
```

## <span data-ttu-id="f0205-127"><a id="howtocreatecode"></a>방법: 코드를 만들어 전화 걸기</span><span class="sxs-lookup"><span data-stu-id="f0205-127"><a id="howtocreatecode"></a>How to: Create the code to make the call</span></span>
<span data-ttu-id="f0205-128">사용자가 양식을 다 작성하면 호출되는 다음 코드는 통화 메시지를 만들고 통화를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="f0205-128">The following code, which is called when the user completes the form, creates the call message and generates the call.</span></span> <span data-ttu-id="f0205-129">이 예제에서는 코드가 양식 단추의 onclick 이벤트 처리기에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0205-129">In this example, the code is run in the onclick event handler of the button on the form.</span></span> <span data-ttu-id="f0205-130">(아래 코드에서 `accountSID` 및 `authToken`에 할당된 자리 표시자 값 대신 Twilio 계정 및 인증 토큰을 사용하십시오.)</span><span class="sxs-lookup"><span data-stu-id="f0205-130">(Use your Twilio account and authentication token instead of the placeholder values assigned to `accountSID` and `authToken` in the code below.)</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
using Twilio;
using Twilio.Http;
using Twilio.Types;
using Twilio.Rest.Api.V2010;

namespace WebRole1
{
    public partial class _Default : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {

        }

        protected void callpage_Click(object sender, EventArgs e)
        {
            // Call porcessing happens here.

            // Use your account SID and authentication token instead of
            // the placeholders shown here.
            var accountSID = "ACNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN";
            var authToken =  "NNNNNNNNNNNNNNNNNNNNNNNNNNNNNNNN";

            // Instantiate an instance of the Twilio client.
            TwilioClient.Init(accountSID, authToken);

            // Retrieve the account, used later to retrieve the
            var account = AccountResource.Fetch(accountSID);

            this.varDisplay.Items.Clear();

            if (this.toNumber.Text == "" || this.message.Text == "")
            {
                this.varDisplay.Items.Add(
                        "You must enter a phone number and a message.");
            }
            else
            {
                // Retrieve the values entered by the user.
                var to = PhoneNumber(this.toNumber.Text);
                var from = new PhoneNumber("+14155992671");
                var myMessage = this.message.Text;

                // Create a URL using the Twilio message and the user-entered
                // text. You must replace spaces in the user's text with '%20'
                // to make the text suitable for a URL.
                var url = $"http://twimlets.com/message?Message%5B0%5D={myMessage.Replace(" ", "%20")}";
                var twimlUri = new Uri(url);

                // Display the endpoint, API version, and the URL for the message.
                this.varDisplay.Items.Add($"Using Twilio endpoint {
                }");
                this.varDisplay.Items.Add($"Twilioclient API Version is {apiVersion}");
                this.varDisplay.Items.Add($"The URL is {url}");

                // Place the call.
                var call = CallResource.create(to, from, url: twimlUri);
                this.varDisplay.Items.Add("Call status: " + call.Status);
            }
        }
    }
}
```

<span data-ttu-id="f0205-131">전화가 걸리고 Twilio 끝점, API 버전 및 통화 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0205-131">The call is made, and the Twilio endpoint, API version, and the call status are displayed.</span></span> <span data-ttu-id="f0205-132">다음 스크린샷은 샘플 실행의 결과를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f0205-132">The following screenshot shows output from a sample run.</span></span>

![Twilio 및 ASP.NET을 사용하는 Azure 통화 응답][twilio_dotnet_basic_form_output]

<span data-ttu-id="f0205-134">TwiML에 대한 자세한 내용은 [http://www.twilio.com/docs/api/twiml][twiml]에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0205-134">More information about TwiML can be found at [http://www.twilio.com/docs/api/twiml][twiml].</span></span> <span data-ttu-id="f0205-135">&lt;Say&gt; 및 기타 Twilio 동사에 대한 정보는 [http://www.twilio.com/docs/api/twiml/say][twilio_say]에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0205-135">More information about &lt;Say&gt; and other Twilio verbs can be found at [http://www.twilio.com/docs/api/twiml/say][twilio_say].</span></span>

## <span data-ttu-id="f0205-136"><a id="nextsteps"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="f0205-136"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="f0205-137">이 코드는 Azure에서 ASP.NET 웹 역할의 Twilio를 사용하는 기본 기능을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f0205-137">This code was provided to show you basic functionality using Twilio in an ASP.NET web role on Azure.</span></span> <span data-ttu-id="f0205-138">Azure를 프로덕션에 배포하기 전에 더 많은 오류 처리 또는 기타 기능을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0205-138">Before deploying to Azure in production, you may want to add more error handling or other features.</span></span> <span data-ttu-id="f0205-139">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f0205-139">For example:</span></span>

* <span data-ttu-id="f0205-140">웹 양식을 사용하는 대신, Azure Blob 저장소 또는 Azure SQL 데이터베이스 인스턴스를 사용하여 전화 번호 및 통화 텍스트를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0205-140">Instead of using a web form, you could use Azure Blob storage or an Azure SQL Database instance to store phone numbers and call text.</span></span> <span data-ttu-id="f0205-141">Azure에서 Blob 사용에 대한 자세한 내용은 [.NET에서 Azure Blob Storage 서비스를 사용하는 방법][howto_blob_storage_dotnet]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f0205-141">For information about using Blobs in Azure, see [How to use the Azure Blob storage service in .NET][howto_blob_storage_dotnet].</span></span> <span data-ttu-id="f0205-142">SQL Database 사용에 대한 자세한 내용은 [.NET 응용 프로그램에서 Azure SQL Database를 사용하는 방법][howto_sql_azure_dotnet]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f0205-142">For information about using SQL Database, see [How to use Azure SQL Database in .NET applications][howto_sql_azure_dotnet].</span></span>
* <span data-ttu-id="f0205-143">양식에서 값을 하드 코딩하는 대신, `RoleEnvironment.getConfigurationSettings`를 사용하여 배포 구성 설정에서 Twilio 계정 ID 및 인증 토큰을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0205-143">You could use `RoleEnvironment.getConfigurationSettings` to retrieve the Twilio account ID and authentication token from your deployment's configuration settings, instead of hard-coding the values in your form.</span></span> <span data-ttu-id="f0205-144">`RoleEnvironment` 클래스에 대한 자세한 내용은 [Microsoft.WindowsAzure.ServiceRuntime Namespace][azure_runtime_ref_dotnet]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f0205-144">For information about the `RoleEnvironment` class, see [Microsoft.WindowsAzure.ServiceRuntime Namespace][azure_runtime_ref_dotnet].</span></span>
* <span data-ttu-id="f0205-145">[https://www.twilio.com/docs/security][twilio_docs_security]에서 Twilio 보안 지침을 읽으세요.</span><span class="sxs-lookup"><span data-stu-id="f0205-145">Read the Twilio Security Guidelines at [https://www.twilio.com/docs/security][twilio_docs_security].</span></span>
* <span data-ttu-id="f0205-146">[https://www.twilio.com/docs][twilio_docs]에서 Twilio에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="f0205-146">Learn more about Twilio at [https://www.twilio.com/docs][twilio_docs].</span></span>

## <span data-ttu-id="f0205-147"><a name="seealso"></a>참고 항목</span><span class="sxs-lookup"><span data-stu-id="f0205-147"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="f0205-148">Azure에서 음성 및 SMS 기능을 위해 Twilio를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="f0205-148">How to use Twilio for Voice and SMS capabilities from Azure</span></span>](twilio-dotnet-how-to-use-for-voice-sms.md)

[twilio_console]: https://www.twilio.com/console
[twilio_pricing]: http://www.twilio.com/pricing
[try_twilio]: http://www.twilio.com/try-twilio
[twilio_api]: http://www.twilio.com/voice/api
[verify_phone]: https://www.twilio.com/console/phone-numbers/verified

[twilio_dotnet_basic_form]: ./media/partner-twilio-cloud-services-dotnet-phone-call-web-role/WA_twilio_dotnet_basic_form.png
[twilio_dotnet_basic_form_output]: ./media/partner-twilio-cloud-services-dotnet-phone-call-web-role/WA_twilio_dotnet_basic_form_output.png

[twiml]: http://www.twilio.com/docs/api/twiml



[howto_twilio_voice_sms_dotnet]: /develop/net/how-to-guides/twilio/

[howto_blob_storage_dotnet]: https://www.windowsazure.com/develop/net/how-to-guides/blob-storage/

[howto_sql_azure_dotnet]: https://www.windowsazure.com/develop/net/how-to-guides/sql-database/


[twilio_docs_security]: http://www.twilio.com/docs/security
[twilio_docs]: http://www.twilio.com/docs
[twilio_say]: http://www.twilio.com/docs/api/twiml/say


[azure_runtime_ref_dotnet]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.serviceruntime.aspx
[azure_webroles_get_started]: https://docs.microsoft.com/en-us/azure/cloud-services/cloud-services-dotnet-get-started
