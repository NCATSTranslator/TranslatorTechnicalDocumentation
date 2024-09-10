---
title: Translator Architecture
---

![[../img/translator-banner.jpg|image]]

The Translator system is comprised of five main components, shown in the diagram below 
([[../index#references]]). Knowledge Providers (KPs) contribute domain-specific, high-value
information abstracted from one or more underlying ‘knowledge sources’. Autonomous Relay Agents (ARAs) build upon the 
knowledge contributed by KPs by way of reasoning and inference across KPs. The Autonomous Relay System (ARS) functions
as a central relay station and broadcasts user queries to the broader Translator
ecosystem and, in turn, compiles results. A user interface (UI) is under development and intended to serve as a public UI to the Translator system.
Finally, a Standards and Reference Implementation (SRI) Component provides services and community-based collaboration
guidance related to the development, adoption, and implementation of the standards needed to achieve the overall
implementation goals of the Translator system.

Further details may be found in the 
[**Translator Architecture repository**](https://github.com/NCATSTranslator/TranslatorArchitecture).

![image](https://user-images.githubusercontent.com/26254388/174347804-0412fbd2-f61f-4573-8073-2408c3c41e15.png)

**Figure 1**  High-level overview of the Translator architecture ([[../index#references]]).

## Example Use Case Application

This example use case application is intended to provide a high-level overview of how to translate a user question
into a Translator Reasoner Standard API (TRAPI) query, execute a TRAPI query, and evaluate results.
The specific use case question is: _what drugs treat chronic pain_?

Shown below is the translation of that user question into a TRAPI query.

![image](https://user-images.githubusercontent.com/26254388/174348079-4bf2ff96-db8e-432e-ba5d-7c82475ec821.png)

**Figure 2** Step-by-step translation of a user question into a TRAPI query ([[../index#references]])

In response to the query, Translator provided answers that are known to be treatments for chronic pain such as
ibuprofen. Translator also provided answers that are correct but not terribly interesting or necessarily aligned with
user intent such as caffeine (an adjuvant included in certain pain medication). Also included among Translator answers
to the example query are answers such as naltrexone, an opioid antagonist, which may not be expected by users. In support of naltrexone, Translator
provided evidence and provenance indicating that naltrexone indeed may be used to treat chronic pain, as highlighted
below. Translator evidence and provenance included ranked answers with scores, primary and secondary knowledge sources
behind any assertions, PubMedCentral or PubMed identifiers, and links to abstracts, etc. 

This sort of serendipitous discovery, or unexpected insight, represents the type of scientific discovery that
Translator aims to foster.

![image](https://user-images.githubusercontent.com/26254388/174348255-2ba2d8d3-8f0e-4678-a4d1-997e299b4a1b.png)

**Figure 3** ([[../index#references]])

While the query provided here is simple and intended to be illustrative, more complex queries are possible using TRAPI 
and a variety of Translator operations and workflows.

In terms of impact, Translator is currently being used to promote serendipitous discovery and augment human reasoning 
in a variety of disease spaces, including Fanconi anemia, systemic sclerosis, cystic fibrosis, Parkinson’s disease, 
and drug-induced liver injury.

Further technical details about the components of the Translator architecture are provided within the **[[development-guide/index|Development Guide]]**.
