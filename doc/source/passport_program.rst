.. _passport_program:

The OpenStack Passport Program
==============================

What?
-----

The OpenStack Passport program is a joint initiative between the Public Cloud Working Group and the OpenStack Foundation.

There are 60+ OpenStack public clouds available globally. Armed with an OpenStack Passport, a user will have the ability to easily gain a trial account on any participating cloud.

The passports will be created by the OpenStack Foundation and distributed in both print and digital forms.

Why?
----

To allow the OpenStack Foundation to act as a unified point of entry for public cloud users, and to help public cloud providers grow their userbases.

When?
-----

A low-tech landing page will be implemented for version 0 of the scheme and will be launched in November 2017 at the OpenStack Summit in Sydney.

Version 1 is currently forecast to land in May 2018 in time for the OpenStack Summit in Vancouver.

How?
----

Version 0
^^^^^^^^^

* Landing page promoting various OpenStack-based public clouds that have signed up to the Passport program
* Marketing exercise to raise awareness and guage interest from users and operators
* Foundation understanding the various public cloud operators commercial offerings - sign up process, how much resource they have available, what services are on offer
* The message: "valid for at least XX resources on any participating public cloud for 1 month"
* To avoid value comparison, agree on a minimal amount of resources a token would be valid (it's ok to offer more)+1
* Should be limited in time.
* APPLICATION CRITERIA: OpenStack interop - OpenStack powered as a requirement for Passport program participation (confirm with participants)
* Public clouds report summary usage to the foundation every month or so (preserving personal information disclosure requirements)+1
* Success of this step will determine the rest...

Version 1
^^^^^^^^^

* How to measure utilisation - maybe don't base it on a dollar value, more on usage i.e a set quota of certain number of instances / volumes etc.+1
* Recommendation is that the public cloud operators are responsible for operating and maintaining any kind of centralized (or decentralized - blockchain?) method of token validation / revocation as well as usage tracking.
* Foundation can generate signed tokens that can be validated on each public cloud using a public key
* Local sig validation approach means that tokens can be reused across multiple public clouds, but that's actually not a bad thing
* Public clouds must locally mark tokens as used so that they can't be infinitely reused on their cloud
* Public clouds report summary usage to the foundation every month or so (preserving personal information disclosure requirements)
* Code / token generation
* Unique URL / QR code -- need to find a printer that would be OK printing lots of different QR codes
* Something equivalent to the length of a Windows licensing key
* QR code contains a URL like  http://opensta.ck/?token=25495720598743957495874359874359845984375643509747350987823509473258572390857342095878
* leads to Foundation-hosted static page listing the participating clouds and the token (ready to be copy-pasted)
* Token can be included as a parameter to the various public cloud links
* Keys used to sign codes to be regenerated every ~ 6 months
* Longevity of tokens (6 months, 1year...)
* Is it more complex than it needs to be ?
* Bunch of trial links on a page gets you 90% there. Let's see after step 0 if that level of complexity is actually necessary
* Being able to terminate trial sign-ups in case of capacity issues

Version 2
^^^^^^^^^

TBA


Selection Criteria
------------------

Participating cloud vendors need to meet the following criteria:

1) They must currently offer a free trial for new public cloud users.
2) They must provide a quality user experience, because confusing/longwinded processes dissuade users. There will be a definition of what a quality UX entails soon.
3) They must have a privacy policy, because OpenStack.org will be sending users to sign up directly for their service


implement an official OpenStack graphic and agreed-upon text on your own website's landing page (details TBA);
You are strongly encouraged to get involved with the bi-weekly IRC meetings hosted by the Public Cloud Working Group (more details below);
You acknowledge that participation in the program does not necessarily guarantee traffic or users.

Questions
---------

1. Can you use one passport on multiple clouds?
2. How do you limit the scope of the trial? Preloaded dollar value? VCPU hours? A dict of quotas for all resource types? 