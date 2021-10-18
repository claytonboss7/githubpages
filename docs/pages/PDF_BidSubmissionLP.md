---
layout: default
title: PDF_BidSubmissionLP
parent: pages
---

```<apex:page controller="PDF_BidSubmissionLPController"
  showHeader="false"
  applyBodyTag="false"
  standardStylesheets="false"
  action="{!logInitialBidMemorialization}"
  renderAs="Pdf"
>
  <head>
    <style>
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
        margin-top: 1in;
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
      <c:PDF_BidSubmissionLP />
    </body>
  </html>

</apex:page>```
