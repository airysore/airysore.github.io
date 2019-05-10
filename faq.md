---
layout: page-fullwidth
title: "FAQ"
subheadline: ""
categories:
  - support
breadcrumb: true
max-toc: 2
---
Below consists of a collection of frequently asked questions, as well as their answers. We will endeavour to keep this list updated where possible - Use the contents, to the left of this, to quickly navigate between questions and answers.

If you feel your question isn't covered here, please use the relevant Teams chat to raise further concerns.

## Governance
### Are there any policies or resources I should be aware of?
Below you will find policies & resources which you may find relevant to your work - This is not an exhaustive list and is updated when flagged.

- [Tesco Cryptography Policy](https://tesco.sharepoint.com/sites/Tescopedia/Code.aspx?Id=498)
- [Tesco Cryptography Standards](https://tesco.sharepoint.com/sites/Tescopedia/Code.aspx?Id=492&Source=https://tesco.sharepoint.com/sites/Tescopedia/Standard.aspx)
- [Security Architecture Team Wiki](https://github.dev.global.tesco.org/SecurityArchitecture/Home/wiki)

## RBAC
### How are team members added to subscriptions?
{% include alert type="important" content="**Note:** If requesting a user is added as a 'Contributor' to a **production** subscription, you should also request they are added to 'Readers' - PIM elevation is used in production to provide self-elevating abilities." %}

All requests for access to the tenancy, and to particular subscriptions, is controlled by the AD team through [ZenDesk](https://tescosupportcentre.zendesk.com/agent/). The **82_Enduser_security_Auth_HSC** queue should be used, and the following information provided:

- The @Tesco.com email of the users requiring access
- The subscription's name (e.g. 169-DEV-APP-1)
- Approval from the WL3 that owns the subscription (ideally, the WL3 for the subscription should raise all requests - This will make the process a lot easier)
- The required role level required (Reader or Contributors)

It should be noted that this is only an interim solution. When Access Manager is available, WL3s will have complete control without requiring this process.

For more information on RBAC see [this page](/pages/Cloud/website/getting-started/RBAC/). Please be aware that for **production subscriptions**, users (requiring 'Contributor' access) should be requested to be added to **both** 'Readers' and 'Contributors'. This will enable them to use PIM to elevate where necessary.

## Subscriptions
### I can't see the TescoAzure tenant in the portal
When you're invited to a subscription for the first time, an email is sent to you which is an invitation. You need to click the 'Get Started' button on this email in order to receive access - Without doing this, you will be unable to access the tenant/see it in the tenant switch dialogue.

Expand the below accordion for an example email, as presently sent out on invitation into the TescoAzure tenancy.

{% include collapse width="90%" padding="20px" title="TescoAzure Invitation Email" content="
<br>
![Email Invite](/pages/Cloud/website/images/knowledgebase/Tesco-Azure-Invitation.PNG)
<br>
" %}

### How do I sign in?
You can sign into your Azure portal from [this page](https://portal.azure.com).

When going through this page, select your Tesco account and run through the usual SSO login process.

### DevTest vs Production

Below you can find common queries/comparisons between the two subscriptions and the level of support for each.

|  | DevTest | Production | Notes |
| --- | :---: | :---: | --- |
| SLA |   | ✔ | Not applicable to DevOps or App Insights |
| Microsoft License Fees |   | ✔ | This includes Windows Server, SQL Server, BizTalk, etc |
| Windows 10 | ✔ | ✔ |   |
| Production Workloads |   | ✔ | The &#39;Dev Test&#39; environment is provided for development and testing only. To be used by VS subscribers and by end users providing feedback and acceptance testing. |
| Able to raise support tickets | ✔ | ✔ |   |
| Capacity restrictions during shortages | ✔ |   | If Azure is &#39;full&#39; the DevTest environment will be provided lower priority access to services. The production environment should not be throttled. |
| Running Costs | SQL DB ~45%, Logic App EC ~50%, App Service ~65%, HDI ~80% | Normal | Price is a guide for discussion, not an offer. |

You can find additional information [here](https://azure.microsoft.com/en-gb/pricing/dev-test/)

### Are we able to maintain our current subscriptions?

You should re-enrol and migrate – even if you&#39;re using a Tesco subscription at present.

### What are my default subscription limits?
[This document](https://docs.microsoft.com/en-us/azure/azure-subscription-service-limits) is the best location to determine your subscriptions default limits, which are also sometimes called quotas. The document does not cover all Azure service, but over time will be expanded to cover more of the platform.

We are bundling the following custom limits with Tesco Azure subscriptions:

| Resource | Region | Default Limit | Maximum Limit |
| - | -| - | - |
| VM per series (DSv2 & DSv3) cores per subscription | West Europe | 250  | Contact support |

The following table summarises common default Azure subscription limits as of 1st February 2019:

| Resource | Default Limit | Maximum Limit |
| - | -| - |
| VMs per subscription | 10,000 per Region | 10,000 per Region |
| VM total cores per subscription | 20 per Region | Contact support |
| VM per series (Dv2, F, etc.) cores per subscription | 20 per Region | Contact support |
| Co-administrators per subscription | Unlimited | Unlimited |
| Storage accounts per region per subscription | 200 | 200 |
| Resource Groups per subscription | 980 | 980 |
| Availability Sets per subscription | 2,000 per Region | 2,000 per Region |
| Resource Manager API request size | 4,194,304 bytes | 4,194,304 bytes |
| Tags per subscription | unlimited | unlimited |
| Unique tag calculations per subscription | 10,000 | 10,000 |
| Cloud services per subscription | Not Applicable | Not Applicable |
| Affinity groups per subscription | Not Applicable | Not Applicable |
| Subscription level deployments per location | 800 | 800 |

### How are subscription limits raised?
This can be done by raising a [New Support Request](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade) within the 'Azure Help and Support Center'.

When submitting a request, please keep the following in mind.
* Raise the ticket as **"Severity: C - Minimal Impact"** as uplifts are usually applied within 5 minutes.
* On the **problem details** blade, select **Resource Manager** as the **Deployment Model**.
* If the **Location** drop-down on the **problem details** blade doesn't generate a list of SKUs, then select another region, click the SKU drop-down and then your desired region again to resolve.
* **DSv2** & **DSv3** are the most common types of compute SKUs.

## Resources
### Are there encryption requirements for traffic?
Yes - All resources should adhere to Tesco's Encryption Policy and Standards. For Azure, all traffic within a VNET **should** be encrypted, while all traffic traversing the VNET to an external endpoint **must** be encrypted according to standards.

As part of 'Drop 3', policies will be implemented from a management level which will prevent the use of non-compliant TLS for Azure Web apps (and enforces auditing on non-Azure web services). This release should also provide capabilities to report on unencrypted traffic which has been captured.

See below for the relevant Tesco policies, as held on Tescopedia.
- [Tesco Cryptography Policy](https://tesco.sharepoint.com/sites/Tescopedia/Code.aspx?Id=498)
- [Tesco Cryptography Standards](https://tesco.sharepoint.com/sites/Tescopedia/Code.aspx?Id=492&Source=https://tesco.sharepoint.com/sites/Tescopedia/Standard.aspx)

You can find further information about 'Data Security and Encryption' at the [following page](https://docs.microsoft.com/en-us/azure/security/security-azure-encryption-overview), by Microsoft.

### Are there restrictions to Azure Marketplace (AM)?
To prevent an overly restrictive environment, due to constraints on available limitations, there are presently no restrictions on the content available from AM.

Before making use of AM, teams should consider whether its use satisfies Tesco's strategic approach to cloud computing, InfoSec requirements and whether it provides stakeholders with best value. Further information on the values behind our cloud approach can be found on the [homepage](/pages/Cloud/website/).

### I'm trying to assign a Public IP (PIP), but it won't let me?
Policies are in place on subscriptions preventing the direct assignment of a PIP to an Azure workload. Teams should not attempt to assign a PIP, unless it's to an [Application Gateway](https://docs.microsoft.com/en-us/azure/application-gateway/overview), [Load Balancer](https://docs.microsoft.com/en-us/azure/load-balancer/load-balancer-overview) or an equivalent. Any exceptions to this rule would require authorisation from the InfoSec and Cloud Platform teams.

All PIPs created are audited, as part of policy compliance.

### Is there a standard in place for product usage?

Guidelines will be created, however at present there is no standardisation provided. Engineering teams are free to choose from the options available on the Azure platform.

### Which region should resources be created in?

| **Subscription** | **Region** |
| --- | --- |
| Dev/Test | EU West |
| Production | EU West and EU North |

### HUB-Spoke – What services can sit in the HUB or Spoke?

Application teams may only deploy to a spoke, which is in turn connected to the HUB of the region. The primary purpose of the HUB is for connecting to data centres through Express Route and to provide access to the internet.

### Will High and Low Level Design information be shared with engineering teams?

Yes, they will be available for engineering teams for reference. You can presently find detailed architectural diagrams on [this page](/pages/Cloud/website/getting-started/Basic-Networking/#detailed-architecture-diagrams).

### Will workloads/instances be audited?

Not at this time – the responsibility of instances/workloads will be with the WL3 subscription owner.

### I just got my subscription, but it won't let me delete resources?  
During the creation of a subscription, the process automatically provisions a number of base-resources required for the HUB-Spoke model to work. To protect against deletion, 'CanNotDelete' locks are automatically added to the 'ResourceGroups' associated with the deployment - These cannot be deleted.

If, however, you're attempting to delete a resource which you've just deployed, check the following:
- A 'Lock' on the resource may be affecting your ability to change the resource. You can check this by navigating to the resource in the portal, and looking under the 'Lock' category. If a lock exists, these may only be removed by the 'Owner' of the subscription.
- You have the requisite level of permission to perform the action.

## Virtual Machines
### Which VM SKUs are allowed?

Teams are free to choose which SKUs to use, however policies are in place to prevent the use of long-lease instances (these will require a business justification). Given the freedom afforded, teams are encouraged to use a common sense approach - Use SKUs which are only necessary for the workload being performed.

## Networking
### Which options exist to provide connectivity to Tesco data centres? Is there AWS connectivity?

Express route is the only option available for connectivity to Tesco DC in Prod Environment only. API&#39;s exposed via Apigee/Akamai are available in dev/test subscription as well

You can presently access AWS by leveraging the direct connect available within Tesco&#39;s DC, through the express route. As an alternative, you may also utilise internet connectivity between the two providers. This connectivity can be used to integrate with pre-existing APIs within AWS, however a connection through Apigee/Akamai is preferred.

### Is it possible to request a great IP allocation?

Yes.

At present this is manually requested through using [this form](/pages/Cloud/website/assets/uploaded-files/IP%20Justification%20Form.docx). Once completed, it should be sent to [Simon Billis](mailto:simon.billis@tesco.com). All requests should have a valid justification or they will not be accepted.

It should be noted that if you are requesting a larger address space, on an already provided subscription, you should also include the current available IPs in the form (ergo, an extra 100 IPs would equate to a total IP count of 607 as by default teams are provided 507).

### I've got my subscription; can I modify the default VNET?
Each subscription has a VNET which has an address space to be used by your subscription. You should use the allocated address space in the VNET.

You should **not** modify the VNET's address spaces (or delete the VNET), as this action may impact other teams, and the operation of HUBs. Modifications can be made to the subnets of your assigned VNET, however each subnet created will lose 5 IP addresses - This is because Azure reserves five IP addresses (last one and first four).  

### I'm trying to use an AppGateway v2, however unable to add a UDR without an error?
Unfortunately, at present (12th February 2019), this is a known limitation of V2 AGs. If you require the use of UDRs, you should make use of a V1 AG - The issue with V2 AG is currently being tracked [here](https://github.dev.global.tesco.org/Cloud/AzureTesco-Infrastructure/issues/44).

## Support
### Are there any chats, on Microsoft Teams, which I&#39;m able to be a part of?

Yes, please refer to the below table. While Mattermost channels do exist, the majority of people are now using Teams – If you do not use Teams, you may miss out on information.

| **Area** | **Link** |
| --- | --- |
| Queries | [Azure User Group](https://teams.microsoft.com/l/channel/19%3aa3cf2763618f43ddbed2566401a5b09c%40thread.skype/Azure%2520User%2520Group?groupId=e7278815-6a55-422b-83e8-12b2d9e45aba&tenantId=3928808b-8a46-426b-8f87-051a36bb2f91) |

### Who are the key contacts within Tesco? Who do I request subscriptions with?

| **Area** | **Contact** |
| --- | --- |
| Subscription Creation | Mark Costello |
| Technical Support | Microsoft Service Request (Premier) |

### Where can I find more information on Akamai, Apigee and APIs?
Please refer to the below for relevant links, dealing with Apigee, APIs and official documentation.

- [API Management FAQ](https://tesco.sharepoint.com/sites/Tescopedia/Code.aspx?Filter=API%20Management%20FAQ) - Find out the answers to frequently asked questions about the Tesco API Management Platform (Apigee Edge).
- [API Quiz & Training Topics](https://tesco.sharepoint.com/sites/Tescopedia/Quiz.aspx)
- [Available Tesco APIs](https://developers.tesco.com/explore)
- [Apigee Training Pages](https://tesco.sharepoint.com/sites/Tescopedia/Code.aspx?Filter=Apigee%20training)
- [Tesco Apigee Portal](https://tesco.login.apigee.com/login)
- [Apigee Documentation](https://docs.apigee.com/)
- [Tesco Apigee Documentation](https://github.dev.global.tesco.org/pages/API-Management/docs/)

### Does Microsoft offer support to engineering teams?

Tesco is covered under the Premier Support plan. For more information, please refer to [this documentation](https://azure.microsoft.com/en-in/support/plans/).

### Who are our contacts within Microsoft?

| **Location** | **Name** | **Email** |
| --- | --- | --- |
| UK | Artis Aramins | [araramin@microsoft.com](mailto:araramin@microsoft.com) |
| UK | Aidan Caffrey | [Aidan.Caffrey@microsoft.com](mailto:Aidan.Caffrey@microsoft.com) |
| India | Goutham Upadhyaya | [Goutham.Upadhyaya@microsoft.com](mailto:Goutham.Upadhyaya@microsoft.com) |

### Are SLAs on PPE environments equivalent to Production?

Yes, provided that this resides inside the production subscription.

## Azure DevOps
### Does Tesco have an Azure DevOps Publisher ID?
At present, the below table outlines the available publisher names and IDs. Using a 'Publisher Id' enables the sharing of additions to DevOps across Tesco, or to outside users (private/public options).

| Name | Publisher ID |
| ---- | ------------ |
| Tesco Plc | TescoPlc |

The publisher, published extensions and membership of the above can be managed [here](https://marketplace.visualstudio.com/manage/publishers/TescoPlc)

Further information on packaging and publishing extensions can be found [here](https://docs.microsoft.com/en-us/azure/devops/extend/publish/overview?view=azure-devops).

## Miscellaneous
### Is X service in AWS available in Azure?

Microsoft provide a full-service comparison as part of their documentation. This can be found [here](https://docs.microsoft.com/en-us/azure/architecture/aws-professional/services) – The majority of services will have a like-for-like Azure equivalent, or multiple.

Commonly requested services and their equivalent include:

| **AWS** | **Azure** |
| --- | --- |
| Lambda | [Functions](https://azure.microsoft.com/services/functions/) &amp; [Event Grid](https://azure.microsoft.com/services/event-grid/) |

### Is there a plan to co-ordinate or move everyone from the existing Aurora setups to Azure?

Not at this time. The current expectation is that teams will move off the Aurora platform by themselves, possibly with cloud platform engineering assistance (NL to confirm)

### Does the present timeline include rolling out to international teams?

The present timeline (June) is primarily for UK and European teams, using EU-West and EU-North – Asia Pacific will follow. At present you will be able request and self-enrol to &#39;DEVTEST&#39; at the end of March – We are unable to provide subscriptions earlier than that outlined.

If you are presently under strict deadlines to build out in the cloud, please approach the Cloud Engineering team directly so that we&#39;re able to determine the best approach for you.

### How do I create a 'Personal Access Token' for GitHub?
GitHub maintain a help page for this topic. You can find more information on the process [here](https://help.github.com/en/articles/creating-a-personal-access-token-for-the-command-line)

### Are there any tools out there that'll make life easier?
Yes, Azure has several interesting tools which you can utilise. Below you can find a few which teams/users have come across.
- [Azure Developer Tools](https://azure.microsoft.com/en-gb/tools/)
- [Azure Resource Explorer](https://resources.azure.com)
- [Azure Visio Stencils](https://www.microsoft.com/en-gb/download/details.aspx?id=41937)
- [Cloud Shell](https://azure.microsoft.com/en-gb/blog/cloudshelleditor/) ([Direct Link](https://shell.azure.com/))
- [Microsoft Learn](https://docs.microsoft.com/en-us/learn/) (Azure learning material; hands on, created by Microsoft.)
- [Azure Reference Architecture](https://docs.microsoft.com/en-us/azure/architecture/reference-architectures/)
- [Azure Quickstart ARM Templates](https://github.com/Azure/azure-quickstart-templates)
- [Terraform Quickstart Templates](https://github.com/terraform-providers/terraform-provider-azurerm/tree/master/examples)
- [Microsoft OpenHack](https://openhack.microsoft.com/#events-calendar) (Hands-on learning events, based around the world)

### I can't get a subscription, but is there a way to test Azure out?
Yes. There is currently a sandbox subscription which you can enrol yourself into - This subscription is scrubbed daily, with various other restrictions in place. This should be used for learning activities only, and should not be used in place of a development or production subscription.

See [this page](https://tesco.sharepoint.com/teams/CloudTransformationProgramme/Pages/AzureScratchPad.aspx) for enrolment.  

### When running commands from within a zScaler protected network, are my requests inspected?
Traffic to Azure is treated the same as any other and is subject to inspection. This has been identified as in issue, especially with services such as KeyVaults - The following URLs are excluded from SSL-inspection.

| URL(s)                                                                       | Use                                   |
|------------------------------------------------------------------------------|---------------------------------------|
| *.vault.azure.net:443<br> management.azure.com:443<br> graph.windows.net:443 | Key Vault management                  |
| login.microsoftonline.com:443                                                | Azure platform authentication         |
