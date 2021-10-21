---
layout: default
title: ChangePasswordController
parent: classes
---
# Metadata Type
classes


# Filename 
ChangePasswordController


# Raw XML
```
/**
 * An apex page controller that exposes the change password functionality
 */
public with sharing class ChangePasswordController {
    public String oldPassword {get; set;}
    public String newPassword {get; set;}
    public String verifyNewPassword {get; set;}        
    
    public PageReference changePassword() {
        return Site.changePassword(newPassword, verifyNewPassword, oldpassword);    
    }     
    
   	public ChangePasswordController() {}
}
```


# Last Modified


# Usage
