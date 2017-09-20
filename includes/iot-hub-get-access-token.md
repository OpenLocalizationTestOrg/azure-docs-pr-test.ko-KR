## <a name="obtain-an-azure-resource-manager-token"></a><span data-ttu-id="63330-101">Azure Resource Manager 토큰 가져오기</span><span class="sxs-lookup"><span data-stu-id="63330-101">Obtain an Azure Resource Manager token</span></span>
<span data-ttu-id="63330-102">Azure Active Directory는 Azure 리소스 관리자를 사용하여 리소스에서 수행하는 모든 작업을 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="63330-102">Azure Active Directory must authenticate all the tasks that you perform on resources using the Azure Resource Manager.</span></span> <span data-ttu-id="63330-103">아래의 예는 암호 인증을 사용하며, 다른 방법은 [Azure Resource Manager 요청 인증][lnk-authenticate-arm]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="63330-103">The example shown here uses password authentication, for other approaches see [Authenticating Azure Resource Manager requests][lnk-authenticate-arm].</span></span>

1. <span data-ttu-id="63330-104">Program.cs의 **Main** 메서드에 다음 코드를 추가하여 응용 프로그램 ID 및 암호를 사용해 Azure AD에서 토큰을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="63330-104">Add the following code to the **Main** method in Program.cs to retrieve a token from Azure AD using the application id and password.</span></span>
   
    ```
    var authContext = new AuthenticationContext(string.Format  
      ("https://login.microsoftonline.com/{0}", tenantId));
    var credential = new ClientCredential(applicationId, password);
    AuthenticationResult token = authContext.AcquireTokenAsync
      ("https://management.core.windows.net/", credential).Result;
   
    if (token == null)
    {
      Console.WriteLine("Failed to obtain the token");
      return;
    }
    ```
2. <span data-ttu-id="63330-105">**Main** 메서드의 끝에 다음 코드를 추가하여 토큰을 사용하는 **ResourceManagementClient** 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="63330-105">Create a **ResourceManagementClient** object that uses the token by adding the following code to the end of the **Main** method:</span></span>
   
    ```
    var creds = new TokenCredentials(token.AccessToken);
    var client = new ResourceManagementClient(creds);
    client.SubscriptionId = subscriptionId;
    ```
3. <span data-ttu-id="63330-106">사용하고 있는 리소스 그룹에 대한 참조를 만들거나 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="63330-106">Create, or obtain a reference to, the resource group you are using:</span></span>
   
    ```
    var rgResponse = client.ResourceGroups.CreateOrUpdate(rgName,
        new ResourceGroup("East US"));
    if (rgResponse.Properties.ProvisioningState != "Succeeded")
    {
      Console.WriteLine("Problem creating resource group");
      return;
    }
    ```

[lnk-authenticate-arm]: https://msdn.microsoft.com/library/azure/dn790557.aspx