---
layout: default
title: SiteLoginController
parent: classes
---
# Metadata Type
classes


# Filename 
SiteLoginController


# Raw XML
```
/**
 * An apex page controller that exposes the site login functionality
 */
global with sharing class SiteLoginController {
    global String username {get; set;}
    global String password {get; set;}

    global PageReference login() {
        String startUrl = System.currentPageReference().getParameters().get('startURL');
        return Site.login(username, password, startUrl);
    }
    
   	global SiteLoginController () {}
}
```


# Last Modified


# Usage
