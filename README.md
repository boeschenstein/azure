# Azure

## Get Subscription to another user

1. Login to the first user, which has a subscription
2. Open Subscription, add another user as contributor (in `Access Control (IAM)`)
3. The other user must get an invitation link, where he must click the `Accept Invitation`. If not available: go to Azure Active Directory, select the user, resend invitition (Identity, Invitation accepted: manage)
4. Optional:
  - Elevate user as co-admin
  - To allow creation of new App Registrations (in Azure Active Directory)
    - open AD Roles and Administrators
    - select Role "Application developer"
    - add the user to this role

Details see: https://blog.atwork.at/post/Invite-external-users-to-your-Azure-subscription
