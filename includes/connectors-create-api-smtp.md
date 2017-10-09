### <a name="prerequisites"></a><span data-ttu-id="82381-101">필수 조건</span><span class="sxs-lookup"><span data-stu-id="82381-101">Prerequisites</span></span>
* <span data-ttu-id="82381-102">[SMTP](https://wikipedia.org/wiki/Simple_Mail_Transfer_Protocol) 계정</span><span class="sxs-lookup"><span data-stu-id="82381-102">A [SMTP](https://wikipedia.org/wiki/Simple_Mail_Transfer_Protocol) account</span></span>  

<span data-ttu-id="82381-103">SMTP 계정 논리 앱에서을 사용 하려면 먼저 hello 논리 앱 tooconnect tooyour SMTP 계정에 권한을 부여 해야 합니다. 다행히 hello Azure 포털에서 논리 앱 내에서이를 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82381-103">Before you can use your SMTP account in a logic app, you must authorize hello logic app tooconnect tooyour SMTP account.Fortunately, you can do this easily from within your logic app on hello Azure Portal.</span></span>  

<span data-ttu-id="82381-104">다음과 같습니다. hello 단계 tooauthorize 논리 앱 tooconnect tooyour SMTP 계정</span><span class="sxs-lookup"><span data-stu-id="82381-104">Here are hello steps tooauthorize your logic app tooconnect tooyour SMTP account:</span></span>  

1. <span data-ttu-id="82381-105">toocreate hello 논리가 응용 프로그램 디자이너에는 연결 tooSMTP 선택 **표시 Microsoft 관리 되는 Api** hello 드롭 다운 목록 다음 입력 *SMTP* hello 검색 상자에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82381-105">toocreate a connection tooSMTP, in hello logic app designer, select **Show Microsoft managed APIs** in hello drop down list then enter *SMTP* in hello search box.</span></span> <span data-ttu-id="82381-106">Hello 트리거나 toouse 만드는 것이 작업을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="82381-106">Select hello trigger or action you'll like toouse:</span></span>  
   ![](./media/connectors-create-api-smtp/smtp-1.png)  
2. <span data-ttu-id="82381-107">하기 전에 모든 연결 tooSMTP을 만들지 않은 경우 SMTP 자격 증명된 tooprovide를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82381-107">If you haven't created any connections tooSMTP before, you'll get prompted tooprovide your SMTP credentials.</span></span> <span data-ttu-id="82381-108">이러한 자격 증명 사용된 tooauthorize 하 여 논리 앱 tooconnect 되며 SMTP 계정의 데이터에 액세스:</span><span class="sxs-lookup"><span data-stu-id="82381-108">These credentials will be used tooauthorize your logic app tooconnect to, and access your SMTP account's data:</span></span>  
   ![](./media/connectors-create-api-smtp/smtp-2.png)  
3. <span data-ttu-id="82381-109">Hello 연결 만들었으며 했으면 이제 다른 hello로 무료 tooproceed 논리 앱에서 단계를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="82381-109">Notice hello connection has been created and you are now free tooproceed with hello other steps in your logic app:</span></span>  
   ![](./media/connectors-create-api-smtp/smtp-3.png)  

