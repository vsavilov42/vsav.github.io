---
layout: single
title: Phishing -- SPF, DKIM and DMARK
date: 2024-02-23
classes: wide
header:
    icon: /assets/images/phishingRegistry/phishingMain.PNG
categories:
  - Phishing
tags:
  - Theory
  - Phishing
  - BlueTeam
---

This post is for explain the differences between SPF, DKIM and DMARK in emails to validate them.

## General concept

The SPF, DKIM and DMARC authentication protocols or records can help us prevent emails from being sent impersonating our identity, an activity known as phishing. They also serve to provide more security to the destination servers of our emails and thus avoid, as far as possible, being marked as spam.

## SPF

The Sender Policy Framework, or SPF, is responsible for certifying which IPs can send mail using the domain in question.

```
Example:
  v=spf1 a mx ~all

- a -> IP Authoriced to send emails.
- mx -> We allow sending emails from the IPs of the domain's mx records.
- ~ -> Called softfail, indicates that mail may sometimes be sent from another unspecified IP. The mail is accepted, but possibly as spam.
```

## DKIM

DomainKeys Identified Mail, is a registry that allows you to sign mail with your domain using public keys indicated in the zones of your domain.

## DMARK

Domain-based Message Authentication, Reporting and Conformance, or DMARC, which complements SPF and DKIM. This log indicates what to do when previous logs fail, so that necessary measures can be taken as soon as possible.
```
v=DMARC1; p=quarantine;
rua=mailto:example@example.com;
ruf=mailto:example@example.com

v= Is the name of the registry, in this case DMARC1.
p= We indicate what you want to be done with our emails. It could be: reject, quarantine or none.
 - reject: Reject all emails that do not meet DMARC checks.
 - quarantine: Emails that fail will be quarantined. They will go to the spam/junk email folder.
 - none: Monitors results, with no action taken on messages that fail.
 - rua/ruf= reference the way in which reports of detected errors are requested to be sent.
 - rua: used when we need a general report.
 - ruf: used when we want to receive complete messages that fail.
```