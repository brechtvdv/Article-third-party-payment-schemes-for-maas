## Third-party payment specification
{:#ttp}

The TPP specification[](cite:cites tpp) describes how local governments can provide trip compensation through MaaS. Inspired by projects like the Mobility Data Specifications ([MDS](cite:cites mds)) and [LBLOD](cite:cites subsidymeasurement), it provides a standards-based method to express subsidy measurements in a machine-readable format and how MaaS providers can validate their trips in an automated fashion. We will first give an overview ([](#ttpdiagram)) of all the steps that need to be performed and give more details in the next subsections. 

The system starts with the local government (agency), that defines which trips can be compensated. When a MaaS provider is found that can implement the subsidy for the city and conforms with the quality framework (QF) criteria, a setup agreement can be arranged. This agreement is annotated, according to LBLOD, with the machine-readable description of the subsidy measurement. After a user has performed a trip with the MaaS app, the trip is mapped in line with the OSLO trips and offer AP and can be validated with the annotated agreement. When this meets the criteria, the validator returns how much can be compensated. The MaaS provider reports the number of trip compensations in order that the agency can reimburse the MaaS provider back. This system meets the requirement of a third-party payment system, because a traveller will only need to pay any remaining amount for the trip and the third-party can define under which criteria a compensation may occur.

<figure id="ttpdiagram" style="display:flex; flex-wrap:wrap">
<center>
<img src="img/tppdiagram.png" width="399px" style="min-width: 50%; flex:1; border: none; box-shadow: none;">
</center>
<figcaption markdown="block">
Overview of the steps an agency (top row) and MaaS provider (bottom row) needs to perform to setup a TPP scheme. After signing an agreement, the MaaS provider compensates trips after mapping and validating a users’ trip with the criteria of the subsidy measurement.
</figcaption>
</figure>

### Agreement

A template for an agreement is provided that agencies can use to set up a TPP system with a MaaS provider. It contains 5 articles that describe:

- the criteria that a trip must comply to for compensation
- that extra costs behold to the user
- billing happens on a quarterly basis based on an anonymized report of the compensation usage. This can of course be changed to, for example every month.
- commitment to promote the TPP system to its residents and visitors
- duration and cancellation

For the criteria, the agency needs to fill in the means of transport (e.g. bike sharing system, train etc.) that must have been used during a trip. Also, its location is implicitly indicated with the administrative boundaries of the agency that initiates the agreement. Furthermore, the agency can set a fixed number of Euros that will be repaid to the MaaS provider when a trip meets the criteria. The duration is currently set to one year and renews automatically with one year. Another possibility would be to work with a fixed start and end date. A notice to cancel the agreement must be made at least 30 days before renewal.

### Agency

The agency can apply a qualification framework to support their decision when selecting the most appropriate MaaS provider(s). This is not part of the template, but criteria that could be part of this are:

- Integration: are all the mobility providers (shared mobility and public transport) that are active in the city integrated into the MaaS application?
- Multimodal: are at least 3 modalities supported besides public transport? 
- Service level: is there a system for handling complaints and does it support Dutch and English?
- Level of service: are subscription formulas or societal beneficial integrations such as third-party payment schemes supported? 
- Availability: is the availability of shared mobility resources displayed in real time?
- Booking: is this available for B2C and does it support pay-as-you-go?

A user story mapping workshop has been organised on 4th September 2019 with the partners of the [MoDi](cite:cites modi) project. There it was clear that agencies want to offer compensations for at least certain means of transport, inside a certain location and for a certain time. Another important aspect is that agencies should be able to chain these criteria together so multimodal behaviour can be promoted. For example, remote municipalities can attract visitors that do not own cars by giving compensation when they take the train to the nearest station and then renting an electric bike for the last-mile travel.

Similarly to MDS that clarifies the structure of the JSON data that must be provided by specifying the fields in a table, we provide a JSON-LD template with corresponding table for each object. The agency (and the MaaS provider in the next section) needs to provide this for objects such as SubsidyMeasurement, Payment and RouteSegmentRequirement. This way, developers do not need to understand semantic technologies to get started and only need to fill in some fields. It is semantically interoperable with the OSLO and LBLOD APs through the JSON-LD context that is added. The subsidy measurement links to the criteria, which contains one or more requirements that must be validated with, and the payment that can be compensated. In [](#requirement), we give an example of a completed requirement for shared bikes in Leuven. It is possible to support multimodality by adding a criterion for every means of transport.

<figure id="requirement" class="figure">
 ````/code/requirement.jsonld````
<figcaption markdown="block">
A traveller is eligible for a subsidy measurement when he uses a shared bicycle within the centre of Leuven and on a monday during rush hours.
</figcaption>
</figure>

### Provider

Providers that signed an agreement with an agency need to map every trip to the OSLO mobility standard for trips and offers in order to use a shared validator. The route that has been executed during the trip is split into several route segments. The latter needs to be specified with the time of departure and arrival, the GPS telemetry, the price and which transport system is used. [](#routesegment) demonstrates this for a route segment that used a shared bike system during rush hours and has cost 8.2 Euros without TPP compensation involved. If the telemetry is located within the centre of Leuven, then it complies with the route segment requirement of [](#requirement).

<figure id="routesegment" class="figure">
 ````/code/routesegment.jsonld````
<figcaption markdown="block">
This route segment is performed during rush hours in the centre of Leuven with a shared bike system. The location data is omitted for space savings.
</figcaption>
</figure>

With the standardized description of a trip and subsidy measurement as expected input, an Open Source validator is being developed that MaaS providers can incorporate into their software. This way, they do not need to implement subsidy measurements themselves, validation happens internally (privacy-sensitive trip data remains on the server) and more complex criteria for the needs of agencies can be implemented in the future without raising the complexity for MaaS providers. The validator is written in Node.js and can be invoked through the Command Line Interface (CLI). It returns whether a trip conforms with the subsidy measurement and how much compensation can be given. In future work, we will provide a programmatic API and publish it on the NPM registry for easier adoption. We also are looking into wrapping this with a Web API and offer this as a Docker container.

