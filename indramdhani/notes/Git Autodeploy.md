# Git Autodeploy

### Auto Deploy TODO

-   Make sure kh.dev.test gitlab account is a member of the repo (go to _Settings →_ _Members_ to check it.
-   Make sure the branch that will be used is protected. ( go to _Settings → Repository → Protected Branches_ to check it\*),\*
-   Add the variable below in the repository _Settings →CI / CD → Variables_ section. Make sure the protected state is enabled.
-   Clone the repo in to the Dev server.
-   Check the `git-deploy.sh` and make sure the directory and repo to pull is correct.
-   Add `git-deploy.sh` and `gitlab-ci.yml` to the repo.
-   Use Gitlab variables to set the auto deploy easier.

Please note that the code/settings are only to auto-deploy the changes to the dev server. You can modify it per requirement.

### Slack Notification TODO

-   In the Integration Settings page of the repo (go to _Settings → Integrations_).
    
-   Find and open _Slack notifications_, fill the fields in _Trigger_ section with Slack channel name.
    
-   Fill the _Webhook_ field with
    
    -   Agency:
        
        ```bash
        https:*//hooks.slack.com/services/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*
        ```
        
    -   Paperlust:
        
        ```bash
        https:*//hooks.slack.com/services/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*
        ```
        
-   Test the setting then save it
    

---

The files are available here

[](http://url.kraftha.us/gitlab-autodeploy)[http://url.kraftha.us/gitlab-autodeploy](http://url.kraftha.us/gitlab-autodeploy)

#git #server #ci/cd