# BAM — Bearer-Agnostic Mesh

BAM is a decentralised communications layer for off-grid environments. It data exchange without cellular networks, internet access, or central servers by forming an opportunistic mesh over whatever local connectivity is available.

BAM is designed for environments where connectivity is intermittent, infrastructure cannot be assumed, and reliability must be achieved without trusting the network.

---

## What BAM is

BAM is a bearer-agnostic, delay-tolerant mesh for low-throughput data exchange. Devices enrol into a shared mission group and become peers in a mesh. Data is exchanged opportunistically when peers encounter one another within the mesh and data will be carried and forwarded through intermediate devices until it reaches its destination or expires. The mesh logic is independent of the underlying transport. BAM can operate over Bluetooth, peer-to-peer Wi-Fi, sidecar radios, or any bearer capable of supporting a bidirectional byte stream.

## What BAM is NOT

BAM is not an app or an answer to how to securely communicate with your peers, it is a communications methodology. Each message carries an application-defined payload identified by an application ID. BAM handles identity, encryption, forwarding, acknowledgements, and expiry. Applications define payload format and semantics. 

---

## Features
BAM is designed to maximise realistic delivery probability in hostile or constrained environments. Reliability is achieved through:
- local persistence of messages
- opportunistic multi-hop forwarding
- end-to-end acknowledgement (where possible)
- redundant forwarding paths
- strict expiry and eviction rules
- Delivery is best-effort and eventual.
- Messages may be delayed, duplicated, or discarded if they cannot be delivered safely within their lifetime.

Missions are time-bounded. Each mission defines:
- when communication begins
- when all undelivered data must expire
- which bearers are acceptable
- Messages that cannot be delivered before mission expiry are discarded.
- If peers encounter one another after expiry, they are notified that messages were dropped due to timeout.

## Bearers and performance

BAM does not assume a single transport. Different bearers have different characteristics:
- BLE is suitable for text and small messages.
- Bluetooth Classic supports messaging as well as small files and image transfer.
- Peer-to-peer Wi-Fi and IP connectivity via sidecars offers the best throughput and reliability.
- BAM allows missions to specify which bearers are acceptable and prioritised.
- Applications are expected to choose payload sizes and behaviours that match the available bearer.

BAM can support:
- group and private messages
- file and photo transfers
- position reports
- Cursor-on-Target (CoT) data
- Custom mission-specific formats, existing protocols can be encapsulated without modification of BAM.

---

## Security model

BAM assumes an untrusted network and potentially compromised bearers. All payloads are encrypted end-to-end and authenticated. Intermediate nodes can forward data but cannot read or modify it. Security does not depend on the transport.BAM does not provide:
- real-time guarantees
- high-throughput streaming
- protection from traffic analysis
- immunity to denial-of-service by authorised participants
- recovery from physical device compromise or application layer vulnerabilities

BAM treats connectivity as an opportunity rather than a guarantee and is designed for unstable links and untrusted, unreliable infrastructure. The result is a resilient, flexible mesh that prioritises security and realistic reliability in denied environments over speed.


## Licence

MIT License
