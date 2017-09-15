### <a name="prerequisites"></a><span data-ttu-id="0873c-101">필수 조건</span><span class="sxs-lookup"><span data-stu-id="0873c-101">Prerequisites</span></span>
* <span data-ttu-id="0873c-102">[SMTP](https://wikipedia.org/wiki/Simple_Mail_Transfer_Protocol) 계정</span><span class="sxs-lookup"><span data-stu-id="0873c-102">A [SMTP](https://wikipedia.org/wiki/Simple_Mail_Transfer_Protocol) account</span></span>  

<span data-ttu-id="0873c-103">논리 앱에서 SMTP 계정을 사용하려면 먼저 SMTP 계정에 연결하도록 논리 앱에 권한을 부여해야 합니다. 다행히 Azure 포털의 논리 앱 내에서 이를 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0873c-103">Before you can use your SMTP account in a logic app, you must authorize the logic app to connect to your SMTP account.Fortunately, you can do this easily from within your logic app on the Azure Portal.</span></span>  

<span data-ttu-id="0873c-104">SMTP 계정에 연결하도록 논리 앱에 권한을 부여하는 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0873c-104">Here are the steps to authorize your logic app to connect to your SMTP account:</span></span>  

1. <span data-ttu-id="0873c-105">논리 앱 디자이너에서 SMTP에 대한 연결을 만들려면 드롭다운 목록에서 **Microsoft 관리 API 표시**를 선택한 다음 검색 상자에 *SMTP*를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0873c-105">To create a connection to SMTP, in the logic app designer, select **Show Microsoft managed APIs** in the drop down list then enter *SMTP* in the search box.</span></span> <span data-ttu-id="0873c-106">사용할 트리거 또는 동작을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0873c-106">Select the trigger or action you'll like to use:</span></span>  
   ![](./media/connectors-create-api-smtp/smtp-1.png)  
2. <span data-ttu-id="0873c-107">이전에 SMTP에 대한 연결을 만들지 않은 경우 SMTP 자격 증명을 제공하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0873c-107">If you haven't created any connections to SMTP before, you'll get prompted to provide your SMTP credentials.</span></span> <span data-ttu-id="0873c-108">이러한 자격 증명을 사용하여 SMTP 계정의 데이터에 연결하도록 논리 앱에 권한을 부여하고 해당 데이터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0873c-108">These credentials will be used to authorize your logic app to connect to, and access your SMTP account's data:</span></span>  
   ![](./media/connectors-create-api-smtp/smtp-2.png)  
3. <span data-ttu-id="0873c-109">연결이 만들어졌으므로 이제 논리 앱의 다른 단계를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0873c-109">Notice the connection has been created and you are now free to proceed with the other steps in your logic app:</span></span>  
   ![](./media/connectors-create-api-smtp/smtp-3.png)  

