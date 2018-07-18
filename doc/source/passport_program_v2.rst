.. _passport_program_v2:

The OpenStack Passport Program v2
==============================

What?
-----

The OpenStack Passport program is a joint initiative between the Public Cloud Working Group and the OpenStack Foundation, and a collaboration effort between OpenStack public clouds.

All participating clouds offering free trial accounts that lets users experience the freedom, performance and interoperability of open source infrastructure around the world. Collectively the OpenStack Passport program represent the broadest public cloud footprint, giving you freedom to deploy your applications across more geographies using the same open source infrastructure.

The OpenStack Passport program also generate and hold coupon codes that are valid on all participating clouds. These codes can and will be distributed at open infra events around the world, events that the Public Cloud Working Group and the OpenStack Foundation see as good strategic events.


Why?
----

To allow the OpenStack Foundation to act as a unified point of entry for public cloud users, and to help public cloud providers grow their userbases.

When?
-----

Plan right now is to release the version 2 of the Passport program at the OpenStack Summit in Berlin - November 2018.

How?
----

* Find developer resources for coupon implementation
* Create guides for member clouds how to keep up with the requirements

Current state
^^^^^^^^^^^^^

First version of the Passport program was released as planned at the Summit in Sydney 2017. 10 public cloud members at launch that offers free trial to cloud users. First cycle until Vancouver Summit 2018 was used as a feedback cycle, to get enough information from users and participating public clouds to be able to make the right design decisions moving forward. 

Future plans
^^^^^^^^^^^^

More filtering
--------------
Add more filtering options, such as:
1) Security standards (potentially) 
2) Service enabled (IPv6, ARM, GPU, FPGA, ...)
3) Business Offering Type (2C, 2B, Research, ...)
    
Regional passports
------------------
Maybe imagine more of a 'regional' passport program
* APAC providers probably don't have interest for US users, vice-versa

Single sign-on
--------------
In the long run, we also would like the openstack.org/passport to be the gate for a single sing-on to all members of the passport program. Still - a lot of things need to sorted out for this to happen - but this would be the ultimate experience (regarding signup) for the end user.
Things that have been discussed:
* Using OpenStack ID for signup
* ....
    

Passport homepage
^^^^^^^^^^^^^^^^^

The homepage for the Passport program is located at www.openstack.org/passport. A landing page promoting various OpenStack-based public clouds that have signed up to the Passport program, as well as describing the Passport program in general.

Features for the Passport homepage are as follow:

1) List of all participating members, including:
2.1) logo
2.2) cloud name 
2.3) description
2.4) Available regions
2.5) Available endpoint/services
2.6) Link to trial page 
2) World map with members plotted 
3) Free text search 
4) Predefined filter options of:
4.1) Regions/locations
4.2) OpenStack versions
4.3) InterOp Powered Standards
5) Information about how you as a public cloud can signup for the Passport program and which requirements that need to be fulfilled

Passport Promotion
^^^^^^^^^^^^^^^^^^
1. OpenStack Foundation to provide promotion via the banner area on the passport homepage
2. Member cloud to promote passport program in their MKT material
3. Passport program lounge at the next OpenStack Summit in Berlin


Passport coupon codes
^^^^^^^^^^^^^^^^^^^^^

High level goal: Be able to hand out unique coupon codes at events - codes that will be valid at any of the members.

The rights to distribute codes belongs to the OpenStack Foundation and to the Public Cloud working group. That includes:
* making decisions of which events they can be handed out at
* to what audience or limitation of number of codes at events

Technical requirements of the solution:
* A code should only be valid once in ONE member cloud - NOT once at MULTIPLE clouds
* A code should have a specific value
* It should be possible to check if code is valid via simple REST API
* It should be possible to invalidate/redeem  a code via simple REST API

Requirements of member clouds:
* Every member cloud need to accept the code format and implement validation and invalidation
* At registration, member cloud is responsible to make sure that coupon codes are invalidated at "passport central database" if user is granted access after screening
* At registration, member cloud is responsible to make sure that coupon codes are NOT invalidated at "passport central database" if user is NOT granted access after screening



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
