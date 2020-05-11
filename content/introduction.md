## Introduction
{:#introduction}

A variety of mobility solutions (bus, bike, step etc.) have taken their place in the public domain space of cities. In Flanders, a new decree for Basic Accessibility (BA) has been installed, which envisions that important social locations must be optimally accessible to travellers. This means that people must be able to combine different mobility solutions easily. Combined mobility should not only be the case for last-mile travel within cities, but also within the whole region of Flanders. So-called Mobi points are being installed on the public domain to make these mobility solutions more physically interoperable. Mobility as a service (MaaS) providers have multiple mobility solutions integrated and are therefore crucial to guide people along the most optimal route, such as the least expensive route.
<span class="placeholder printonly">
<span style="display: block; height: 7em;"></span>
<!-- This is a dummy placeholder for the LNCS first page footnote -->
</span>
Standardized data models ([GTFS](cite:cites gtfs), [MDS](cite:cites mds)) or Web APIs ([GBFS](cite:cites gbfs), [TOMP API](cite:cites tompapi)) allow MaaS to calculate the financial cost of a trip, however, this does not exist for third-party payment (TPP) schemes. A TPP system means that a mobility solution receives compensation directly from a third party, such as a local government, for a trip. Instead of having the traveller to pay the full cost, based on how long or how far a mobility resource is used, a TPP system requires that a traveller only pays any remaining amount for the trip. In exchange for this the third-party should be able to define under which criteria a  compensation occurs. A TPP system can be achieved as a pre- or postpaid system. A prepaid system is mostly implemented as vouchers that a third-party can buy from the mobility solution. Each voucher contains a predetermined value, such as free rides or credit that has been paid in front by the third-party. The latter then gives the vouchers to its target audience, which they can upload on their account. In a postpaid system, the third-party signs an agreement with the mobility solution that certain trips can be compensated. The mobility solution advances the costs and sends afterwards an invoice to the third-party. TPP systems are commonly set up between cities and mobility providers ([](#table-tpp)) and results from a subsidy measurement that the local council decided on. On [](#table-tpp), we see a few examples of TPP systems in the cities Deinze, Leuven and Schoten. A user may get compensation when a trip meets certain criteria, such as a certain means of transport is used, it has taken place between the boundaries of the city or during an event. These are all set up in 1 to 1 agreements, which makes it very difficult for MaaS to discover and incorporate TPP systems in their route planning advice.

<figure id="table-tpp" class="table" markdown="1">

| City      | Description | Provider | Criteria |
| --------- | ----------- | -------- | -------- |
| Deinze    | Free rides with shared bikes | Blue Bike | Location of the trip must be in Deinze |
| Leuven    | Free rides with bus | De Lijn | Citizens younger than 12 years of district Leuven |
| Leuven    | Discount on public transport | NMBS and De Lijn | During certain events |
| Schoten   | Vouchers for 20 minutes free rides with shared bike | Mobit | During certain events | 
| Schoten   | Free rides with bus | De Lijn | During New Year's Eve and Day |

<figcaption markdown="block">
State of play of third-party payment schemes in Flanders
</figcaption>
</figure>

MaaS providers could also set up a TPP system, however, they have multiple mobility providers integrated, which only increases the need for a standardized description of mobility related rules and how they should be validated. For example: one city wants to support shared bikes by offering compensation of 1 Euro for every trip, while the other city wants to support scooters when they use the train beforehand. In this article, we propose a specification for a postpaid TPP system between local governments and MaaS providers. This includes how local governments need to describe their subsidy measurements and how MaaS providers can validate their trips with a subsidy measurement by using a shared validator.

The remainder of this article is structured as follows: we first describe two semantic based application profiles to describe trips and subsidy measurements. Then we explain our proposed TPP system and how this reuses the application profiles. Finally, we conclude how others can deploy our TPP system and explain our next steps.


