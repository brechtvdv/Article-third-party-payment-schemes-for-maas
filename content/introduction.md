## Introduction
{:#introduction}

<!-- A variety of mobility solutions (bus, bike, step etc.) have taken their place in the public domain of cities. In Flanders, a new decree for Basic Accessibility (BA)[](cite:cites ba) has been installed, which envisions that important social locations must be optimally accessible to travellers. This means that travellers must be able to combine different mobility solutions easily. Combined mobility should not only be the case for last-mile travel within cities, but also within the whole region of Flanders. So-called Mobi points are being installed on the public domain to make these mobility solutions more physically interoperable. Mobility as a service (MaaS) providers have multiple mobility solutions integrated and are therefore crucial to guide people along the most optimal route, such as the least expensive route.
-->
<!--<span class="placeholder printonly">
<span style="display: block; height: 7em;"></span>-->
<!-- This is a dummy placeholder for the LNCS first page footnote -->
<!-- </span>-->

Standardized data models ([GTFS](cite:cites gtfs), [MDS](cite:cites mds)) or Web APIs ([GBFS](cite:cites gbfs), [TOMP API](cite:cites tompapi)) allow MaaS providers to calculate the financial cost of a trip, however, this does not exist for third-party payment schemes. The term 'third-party payment' (TPP) refers to the compensation a traveller receives from a third party, such as a local government, when a trip is performed compliant with the third parties' criteria. Such a system can be achieved in a pre- or postpaid fashion. From the view point of a traveller, with prepaid, only a smaller part of the trip must be paid by the traveller; the other part is arranged between the third party and mobility provider. With postpaid, the traveller only gets compensated afterwards. In this article, we will focus on prepaid, being the most convenient for travellers. Prepaid can be implemented with vouchers or mobility budget containing, for example, free rides or credit. Another approach is an agreement describing the criteria and how a mobility provider invoices the third party. Cities already set up agreements with transport providers ([](#table-tpp)) where local decisions define the criteria in the form of subsidy measurements. The overview on [](#table-tpp) shows that criteria are based on location, time, transport modality and profile information. Currently, these TPPs are made ad hoc lowering the discoverability and reusability for route planning advice in MaaS. Therefore, we propose a specification for a prepaid TPP system defining the semantic description of subsidy measurements and trips, and an open-source validator to verify whether a trip is compliant with a subsidy measurement.

<figure id="table-tpp" class="table" markdown="1">

| City      | Description | Provider | Criteria |
| --------- | ----------- | -------- | -------- |
| Deinze    | Free rides with shared bikes | Blue Bike | Location of the trip must be in Deinze |
| Leuven    | Free rides with bus | De Lijn | Citizens younger than 12 years of district Leuven |
| Leuven    | Discount on public transport | NMBS and De Lijn | During certain events |
| Schoten   | Vouchers for 20 minutes free rides with shared bike | Mobit | During certain events | 

<figcaption markdown="block">
State of play of third-party payment schemes in Flanders
</figcaption>
</figure>

<!-- The remainder of this article is structured as follows: we first describe two semantic based application profiles to describe trips and subsidy measurements. Then we explain our proposed TPP system and how this reuses the application profiles. Finally, we conclude how others can deploy our TPP system and explain our next steps. -->


