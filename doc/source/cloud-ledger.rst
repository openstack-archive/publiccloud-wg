..
 This work is licensed under a Creative Commons Attribution 3.0 Unported
 License.

 http://creativecommons.org/licenses/by/3.0/legalcode

==========================================
Cloud Ledger Proposal
==========================================

The original proposal was published in a google doc [0] and shared at Dublin PTG
and Vancouver Summit during Public Cloud WG sessions.


Problem description
===================

The long term goal when Passport Program [1] was proposed is to setup a single
unified entrance for member public cloud freemium offerings.

However this seemingly simple mission statement bears tremendous technical
hurdles. From traditional cloud computing aspect, the solution requires cloud
federation. The Open Infra Foundation would have to act as a central federation
broker point which:
* is able to extract usage information from each of the federated public clouds
for the purpose of billing, statistics and safety net (can't allocate too much
free resource beyond limit of each cloud)
* is able to check authorization in each of the federated public clouds to
ensure there is no multiple spendings of the same promo code.
* is able to provide unique universally accepted promo codes and track the life
cycle of each and everyone of them.

As is well known in the industry today, cloud federation has been approved
very difficult to achieve in real life. The legal and technical difficulties are
almost impossible to overcome.

Use Cases
---------

It would be great to have a solution which:
* could be able to provide a unique universally accepted promo code among member
cloud without the legal and technical overhead.
* could be able to track the usage of the promo code without resolving to a
central broker which needs to talk to the billing and auth system of each cloud.
* could be able to prevent multiple spendings of the same promo code without
resolving to a central broker which needs to talk to the billing and auth system
of each cloud.
* could be able to be done in an energy efficient and laptop workable way.


Proposed Change Overview
========================

The difficulties illustrated above seems like a good fit for the blockchain
technology, or at least certain flavor of it. Therefore a blockchain solution
is proposed here to tackle these problem.

The TL;DR version of the proposal could be described as a Proof of Authority
(PoA) based sidechain solution. The first trial run of the sidechain experiment
will be based upon Ethereum Classic (known as ETC) sidechain proposal.


Technical Background
====================

It is not the purpose of this section to provide a thorough literature research
of the blockchain field. Hence a rudimentary understanding of the blockchain
technology, the concept of mining, and basic knowledge of current major
blockchain solution is required.

PoA Definition
--------------

Below is the explanation from wikipedia [2]:

In PoA-based networks, transactions and blocks are validated by approved account
s, known as validators.Validators run software allowing them to put transactions
in blocks. The process is automated and does not require validators to be
constantly monitoring their computers. It, however, does require maintaining the
computer (the authority node) uncompromised. The term was coined by Gavin
Wood, co-founder of Ethereum and Parity Technologies.

With PoA individuals earn the right to become validators, so there is an
incentive to retain the position that they have gained. By attaching a
reputation to identity, validators are incentivized to uphold the transaction
process, as they do not wish to have their identities attached to a negative
reputation. This is considered more robust than PoS, as:
* In PoS, while a stake between two parties may be even, it does not take into
account each party’s total holdings. This means that incentives can be unbalance
d.
* Meanwhile, PoW uses an enormous amount of computing power, which, in itself
lowers incentive. It is also vulnerable to attack, as a potential attacker would
only need to have 51% of the mining resources (hashrate) to control a network,
although this is not easy to do.

On the other hand, PoA only allows non-consecutive block approval from any one
validator, meaning that the risk of serious damage is minimized.

Some example implementation could be found in [3], [4] and [5].

Why PoA
-------

First of all, since there is requirement of non-PoW consensus, PoS flavored
mechanisms are the best fitted tools.

Secondly, given the character of the problem, the cloud ledger will consist of
nodes run by member public clouds which are known entities, and by end users
which are unknown to the network by nature. The Caliper [6] version of PoS might
not be good choice since we are not targeting totally anonymous nodes which
already have ether assets. PoA is better suited because the nodes run by the
member clouds could serve as the validator since their incentive to make sure
the cloud ledger functioning correctly is stronger than others, and there is no
pre-requisite of digital asset accumulation.

Thirdly, a well engineered PoA governance model could handle requirements like
GDPR very well in contrast to PoW based public blockchains.

Sidechain
---------

Scalability is a well know and hot debated topic in blockchain industry. There
are several schools of thoughts, and the one this proposal subscribed to is the
so-called layer 2 solution. Layer 2 means utilizing an off-chain solution
without modification on the base layer. An opposite example of such solution is
smart contract [7] and sharding proposal [8] in Ethereum.

Lightening Networks [9] and L4's counterfactual state channel [10] are two
examples of layer 2 solution targeting Bitcoin and Ethereum. The essence is that
by having an off-chain channel based settlement, the efficiency as well as the
volume of the transactions could be enhanced without directly touching the base
layer of Bitcoin and Ethereum.

Another layer 2 option, which is utilized in this proposal, is the sidechain[11]
solution. A sidechain is like a distant relative of the mainchain. The sidechain
could have totally different consensus mechanism or token offering plans from
the mainchain. The experiment done in the sidechain will never affect
the mainchain, and if there is value transfer needed, it could be done in atomic
swap. The security of the sidechain could have another level of guarantee via
checkpointing with the mainchain.

To borrow the example of OpenStack, sidechain is like the vendor distros whereas
mainchain is like the upstream community. Any enhancement made in the distro has
no influence on the upstream community, unless the changes are submitted and
merged in the upstream community (atomic swap). On the contrary, smart contract
is like every vendor directly develops its private feature at the upstream. The
upstream will have more commercial desired features implemented and shortened
time to market gap, however with the down side of the upstream got affected with
all the problems these features bring and code base got bloated. Sharding, on
top of it, is like have each vendor only operate on one module of the upstream
code without the integration testing.

The benefit of a sidechain solution also reflects on the governance model. Since
sidechain is free to implement a different model from the mainchain, it is more
flexible and this flexibility will not affect the immutability of the mainchain.

Ethereum Classic
----------------

The reason for choosing ETC [12] as the first trial run mainchain are as follows:
* ETC is preserving the PoW mechanism unlike ETH which is transitioning to a PoS
based blockchain. PoW is the only currently battle proved secure consensus
mechanism for public chains, thus is ideal for a mainchain.
* ETC still preserves many of the original Ethereum important features such as
smart contract. Although many sidechain advocates consider smart contract a
direct threat, a Turing complete language is still vital for things like policy
driven deployment and automation, which are prevalent in cloud computing.
* The dev community is very friendly. ETC is less hyped than many new ICO crazed
solutions as well as the two most established ones: Bitcoin and ETH.

Utility Token VS Security Token
-------------------------------

Many of the hype around blockchain are related to the concept of a token. There
are two types of token, broadly speaking, that could be offered by a blockchain
solution: utility token or security token [13].

The most common ones that people hear everyday is security token. There are
three types of security token:
* Token which were securities legally : e.g SEC interpreted Ether (not Security
after fully decentralized, but could be considered as security at the moment of
the ICO). Many of the existing ICO issued tokens could fall into this category.
* Token which are de facto securities : there are many tokens function as
securities but not recognized by their issuer.
* Tokenized security : This is something interesting in the future.

Utility tokens are tokens that only represents certain functionality of a
commercial product. Examples are if Starbucks issue a token to serve as promo
cards, this token is a utility token since it only represents the commercial
value of the Starbucks product. If Starbucks stock price changes, the utility
token does not change with it. One cup of coffee is always one cup of coffee.

At the time of the writing, it is still unclear if PoA based Cloud Ledger side
chain needs to issue an ERC20 [14] like token to solve the problem. But if that
were to be the case, the token created is definitely a utility token instead of
a security one. Its value depends upon how the member cloud accepts it and the
overall public cloud industry.

Governance Model
----------------

There are two types of major governance models in the blockchain industry:
on-chain and off-chain. Off-chain governance works in a way which OpenStack
or any other major open source communities are familiar with : people talking
and voting. On-chain governance is a new thing in blockchain where decisions
are made as part of code execution, which means voting is based upon logic
instead of human reasoning. One of the famous example of on-chain governance is
EOS's constitution-attached on-chain model.

For PoA based chains, the governance is mostly needed when a new validator is
added to the chain. Since for Cloud Ledger every validator node represents
a public cloud operator, it would be better to have a hybrid governance model.

Cloud Ledger's hybrid governance model means it involves both off-chain and
on-chain governance. On the granularity of public cloud operators, the public
cloud wg still functions as the main forum for decisions like which public cloud
will join. On the granularity of personal who works for the public cloud,
an open source public notary (something like CNCF TUF/Notary [15]) will be
established to help an on-chain governance procedure to validate if a node ran
from an off-chain agreed cloud provider is indeed operated by a benevolent actor

Trusted Public vs Permissioned
------------------------------

Cloud Ledger mostly confirm to the C2 type defined in ECIP-1027 [16] which
is a privately governed public chain. It is privately governed because the
validator nodes are operated from the Passport Program member public clouds. It
is still a public chain because the end users are not pre-determined.

Many wonders the difference between C1 and C2, i.e private chain vs trusted
public chain. The main difference is for a private chain, or a permissioned
blockchain like hyperledger fabric or stl, although every node does not know
each other necessarily, on organizational level they do. For example a banking
private chain could consist nodes that represent different branches that is
unaware of each other, however the participating banks knows each other and thus
forms a consortium blockchain.

For Cloud Ledger like C2 chains, only part of the network (e.g validator nodes
in this example) is governed by known parties, the rest larger portion of the
network still consist of nodes that the validator nodes will have no idea where
they will come from.

If A Blockchain At All
----------------------

The asymmetry of resource possession (the very nature of public cloud computing,
hosting vs renting) decides the mutability nature of the ledger. However since
sidechain is utilized, the mainchain still remains immutable no matter what
happens on the sidechain.

Thus it is important to point out that cloud ledger has a immutable state record
on the mainchain. From the mainchain's point of view, the sidechain is an
immutable ledger without the knowledge of what happened inside the sidechain. A
wrongly written history could first live at the sidechain but will be rejected
by the mainchain, therefore for mainchain the history of the sidechain state is
consistent all the time, which is a critical difference regarding how DAO attack
was dealt.

If cloud ledger were to be designed as a public chain in its own right, then
by any definition it is not a blockchain at all, a distributed ledger to say the
best.

Exactly because cloud ledger is designed as a sidechain of a public blockchain,
and the above mentioned immutability of sidechain state, cloud ledger is a
valid blockchain solution which could not be replaced by a datacenter oriented
distributed database system, or a permissioned distributed ledger.


Proposed Change Detail
======================

A PoA based ETC sidechain called Cloud Ledger is proposed here to address the
problems. Cloud Ledger is a privately governed public blockchain, of which PoA
validator nodes have to be operated from trusted passport program member clouds,
whereas non-validator nodes are anonymous beforehand.

PoA consensus operates on a mechanism in which validator takes turn (slots) to
sign transaction and validate blocks. Unlike PoW which requires power
consumptive mining or PoS which requires crypto asset accumulation, PoA relies
on incentives of the identity (reputation) of the validator nodes. Moreover
since the Passport Program members are competitors in public cloud industry,
it makes few sense any of them should collude.

PoA guarantees safety from the point of view that malevolent actors could only
affects its slot, instead of something like mining power concentration.

Adds upon that, sidechain provides another level of security by periodically
checkpoints current state fingerprints (a cryptographic hash of the state) to
the mainchain. This means when attack happens (history altered), the mainchain
will quickly notice the attack by rejecting the invalid fingerprints, and side-
chain validators could deploy smart contract that reverse the attack to the
previous valid state.

All the above mentioned proposal is documented in detail in ECIP-1027/1028 [16]
and the ETC poc could be found at [17]

One kind of smart contract ("bootstrap contract") will be needed to deployed on
the sidechain to identify the validator nodes information as well as the
checkpoints configuration, which effectively bootstrap the sidechain network.

Another kind of smart contract ("transact contract") might be needed to define
how a user should request the universal promo code, the total limit on the promo
code issue (could be designed as a pool consists of all the available promo code
quantities of each cloud), the confirmation of the usage of the promo code, the
liveness setting of the promo code, and how should a user transfers this promo
code to another.

In this smart contract the public cloud operator could also design what spec of
the instance might associate with the promo code, since not all types of
instances will be available for the freemium offerings.

An ERC20 compliant token could be issued as a reward for the promo code usage
confirmation.

An implementation example of utilizing ETH Geth for PoA network could be found
at [18].

A hybrid governance model will be used for both off-chain recognition a public
cloud member as well as on-chain confirmation of an effective validator node
from that member. The on-chain governance will involve interactions with a
public notary facility to confirm the proposed new validator node.

Sample Work Flow
----------------

Promo code request workflow :
* By starting the sidechain configured nodes and deploy the bootstrap contract,
the cloud ledger goes on live.
* By applying the transact contract, a user start a request for a Passport
token from the cloud ledger for freemium public cloud resource. Let's say the
user request a promo code corresponding to a low-end instance.
* The execution of the transact contract will check if the request will surpass
the limit. If not the request is successful and the validator assigned at this
time slot will sign the transaction. Later this transaction with others will be
bundled into a new block which the validator will verify and create.
* The user could use the transaction id as the promo code for the free resource
it desires after registration with that public cloud.
* The public cloud will query the cloud ledger node with that transaction id. If
it is a legit one with a valid TTL, the free resource then will be allocated to
the user.
* (optional) The cloud ledger node ran by the public cloud node could apply the
transact contract with the signal of promo code usage confirmation, and an ERC20
compliant token could be sent to the user's address as an reward.

Validator addition workflow :
* There is a new public cloud want to join Passport Program and cloud ledger.
* Public Cloud WG works with Open Infra Foundation verifies the request to join
the Passport Program.
* That new member public cloud will need to add itself to the cloud ledger
notary with the evidence of its passport membership approval.
* After that it bring up a cloud ledger node and update/apply the bootstrap
contract to request adding itself as a new validator node.
* This request kicks off the on-chain governance procedure and once a majority
of current validator node verifies the notary information, this new node will
be recognized as a new validator.

Alternatives
------------

* option 0 : Register to a public cloud and apply for the free stuff as how it
works today. There is absolutely no problem with that and it is probably easier
compared to the blockchain learning curve. However the user will never acquire
a universal promo code and what it means in the long run : a common
market built upon an open source financial infrastructure which minimizes the
frictions Introduced by regulation, technology and many other things.

* option 1 : Adopt traditional centralized cloud federation, it will prove to be
almost impossible for Open Infra Foundation to act as the central broker, as
well as the member clouds to negotiate out an agreement for the cloud federation
both technically and legally.

* option 2 : Adopt a permissioned distributed ledger technology, however since
the consumer of the public cloud computing resource is both unknown beforehand
and unrelated to any public cloud operator themselves, it will prove to be unfit
to use such option.

* option 3 : Adopt a public blockchain technology, however it will be difficult
for the chain to either be energy effective or compliance to regulations such as
GDPR.

* option 4 : Adopt a smart contract method to store information on Ethereum or
Ethereum Classic. It could work as an alternative if we do not concern about
the affect on the mainchain.

* option 5 : Adopt a sidechain method upon Bitcoin. It could work as an
alternative if we do not concern about the benefit brought by smart contract.

* option 6 : Adopt a sidechain method upon Ethereum. It could work as an
alternative if we do not concern about the transition to PoS on the mainchain

* option 7 : Adopt a smart contract or sidechain method on other blockchains.
It could work as an alternative as we will explore more options in the future.


Data model impact
-----------------

No data model impact on the cloud side.

REST API impact
---------------

No REST API impact on the cloud side.

Security impact
---------------

Although the proposed solution has several above-mentioned security advantages,
it should be noted that many of them are remain in theory. There will be more
practical threats when the sidechain is actually deployed. For example although
PoA could have malevolent validator only affects some slots, bad actors
could collude to affect the entire network (switch to the wrong longest chain).

Another possible attack is to drain the network. PoW empowers the time being
used as a restriction, it is just impossible to saturate the network with huge
numbers of transaction requests (also being viewed as a drawback by some
ironically). This is not the case for the PoA networks. Hopefully the design of
the promo code quantity limit, the promo code TTL and the validator sign limit
per slot could help prevent such attack.

The security impact should be continually investigated.

Notifications impact
--------------------

TBD

Other end user impact
---------------------

TBD

Performance Impact
------------------

TBD

Other deployer impact
---------------------

TBD

Developer impact
----------------

TBD


Implementation
==============

Assignee(s)
-----------

Primary assignee:
  zhipengh

Other contributors:
  TBD

Work Items
----------

* Design the cloud ledger smart contracts
* Bring up testnet


Dependencies
============

* Geth sidechain and PoA support


Testing
=======

A testnet will be established for testing.


Documentation Impact
====================

TBD

References
==========
[0] https://docs.google.com/presentation/d/1RYRq1YdYEoZ5KNKwlDDtnunMdoYRAHPjPsln
ng3VqcI/edit?usp=sharing
[1] https://www.openstack.org/passport
[2] https://en.wikipedia.org/wiki/Proof-of-authority
[3] https://medium.com/poa-network/proof-of-authority-consensus-model-with-ident
ity-at-stake-d5bd15463256
[4] https://wiki.parity.io/Proof-of-Authority-Chains
[5] https://github.com/ethereum/EIPs/issues/225
[6] https://eips.ethereum.org/EIPS/eip-1011
[7] https://en.wikipedia.org/wiki/Smart_contract
[8] https://github.com/ethereum/wiki/wiki/Sharding-FAQs
[9] https://lightning.network/
[10] https://medium.com/statechannels/counterfactual-generalized-state-channels-
on-ethereum-d38a36d25fc6
[11] http://www.truthcoin.info/blog/drivechain/
[12] https://ethereumclassic.github.io/
[13] https://blog.nomics.com/flippening/economics-stephen-mckeon/
[14] https://theethereum.wiki/w/index.php/ERC20_Token_Standard
[15] https://github.com/theupdateframework/notary/blob/master/docs/service_archi
tecture.md
[16] https://github.com/ethereumproject/ECIPs/pull/69
[17] https://github.com/ETCDEVTeam/sidekick-doc
[18] https://hackernoon.com/setup-your-own-private-proof-of-authority-ethereum-n
etwork-with-geth-9a0a3750cda8



History
=======


.. list-table:: Revisions
   :header-rows: 1

   * - Stein
     - Introduced
