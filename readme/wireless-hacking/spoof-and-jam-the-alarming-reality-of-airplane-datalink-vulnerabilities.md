---
icon: plane-departure
---

# Spoof-and-Jam: The Alarming Reality of Airplane Datalink Vulnerabilities

## Spoof-and-Jam: The Alarming Reality of Airplane Datalink Vulnerabilities

In today’s aviation industry, seamless and secure communication between pilots and air traffic controllers is vital. As technology evolved, traditional voice communication systems gave way to digital alternatives like **Controller-Pilot Datalink Communications (CPDLC)** and **Automatic Dependent Surveillance–Contract (ADS-C)**. These systems reduce radio congestion and improve operational efficiency — but are they truly secure?

A group of academic researchers from Boston — **Harshad Sathaye, Guevara Noubir, and Aanjhan Ranganathan** — conducted an in-depth security analysis of these aviation datalink applications. Their findings? Deeply concerning.

### What Are CPDLC and ADS-C?

* **CPDLC** allows air traffic controllers to send text-based messages directly to the cockpit, reducing miscommunication from noisy radio channels.
* **ADS-C** automatically shares aircraft position and intent information at predefined intervals or events, helping controllers maintain safe separation in remote areas without radar.

These systems were designed with functionality and efficiency in mind — not necessarily security.

***

### The Attack: Spoof-and-Jam

The researchers demonstrated **"spoof-and-jam"** attacks that can:

* Jam legitimate CPDLC/ADS-C communication.
* Spoof fake but believable messages to pilots or ground stations.
* Suppress or delay delivery of critical instructions or updates.
* Create confusion or influence pilot decisions with high success rates.

Using commodity hardware and software-defined radios, they achieved a **98.85% success rate** in interfering with these communications.

Imagine a scenario where a pilot receives a forged descent clearance or misses a critical reroute due to a jammed uplink — the consequences can be catastrophic.

***

### Key Findings from the Paper

* **Lack of Authentication**: These systems often lack proper authentication and encryption, making it trivial to spoof or intercept messages.
* **Easy to Exploit**: The datalink systems rely on cleartext over VHF or SATCOM, vulnerable to off-the-shelf SDR tools.
* **Poor Detection**: Airlines and ATC may not easily detect spoofed commands or dropped messages in real time.

You can read the full research paper here: [On the Implications of Spoofing and Jamming Aviation Datalink Applications (PDF)](https://lnkd.in/dwgZungV)

***

### What's the Fix?

The researchers urge industry stakeholders to:

* **Integrate cryptographic protections** (encryption, integrity checks).
* **Update standards** from ICAO and aviation manufacturers.
* **Deploy intrusion detection systems** to spot spoofing patterns.
* **Audit and upgrade legacy systems** in a phased, fail-safe manner.

***

### The Bigger Picture

With air traffic increasingly dependent on automated, digital communications, it's critical that **security is not an afterthought**. This paper is not just a warning — it's a wake-up call.

If you’re in the **aviation security space**, consider this a sign: **your systems need hardening**. It’s not just about keeping planes on course — it’s about keeping passengers safe in a world where digital threats are airborne too.



***

## REFERENCES

* [https://aanjhan.com/assets/sathaye22\_acsac.pdf](https://aanjhan.com/assets/sathaye22_acsac.pdf)
