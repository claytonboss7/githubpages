---
layout: default
title: PDF_TraceDashboardBeta
parent: pages
---

```<apex:page controller="TraceDashboardControllerBeta" showHeader="false" applyBodyTag="false" standardStylesheets="false"
  doctype="html-5.0" renderAs="Pdf">
  <apex:stylesheet value="https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css"/>

  <head>
    <style type="text/css">
      @page {
        margin: 1in 0.25in 2in 0.25in;
        font-family: Sans-serif, "Helvetica Neue", Helvetica;
        width: 100%;
        word-break: break-all;
        @top-center {
          content: element(header);
        }
        @bottom-left {
          content: element(footer);
        }
      }

      @page: first {
        margin-top: 0.7in;
        @top-center {
          content: "";
        }
      }

      body {
        font-family: Sans-serif, "Helvetica Neue", Helvetica;
        font-size: 9px;
      }

      div.content {
        position: relative;
      }

      div.footer {
        position: running(footer);
        margin-top: 0px;
      }

      span.page:before {
        content: counter(page);
      }
    </style>
  </head>
  <html>
  <!-- HERE IS THE body OF THE COMPONENT , HOLDS HEADERFOOTER AND BODY COMPONENT -->

  <body>
    <c:PDF_HeaderFooter />

    <!-- HERE IS THE COMPONENT WITH THE BODY -->
    <c:PDF_TraceDashboardBeta />
  </body>

  </html>

</apex:page>```
