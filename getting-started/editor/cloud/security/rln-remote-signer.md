# RLN Remote Signer

Validating Lightning Signer (VLS) is an open-source **Rust library for secure, self-custodial Lightning signers**. Unlike hot wallets or blind signers, VLS keeps your private keys off the node **and** validates each signing request, ensuring only legitimate channel operations are approved. In other words, even if your Lightning node were compromised, funds remain safe thanks to the signer’s rigorous policy checks.

## System Overview

VLS splits Lightning key management into two primary components:

{% stepper %}
{% step %}
### Lightning Node

Runs the usual LN logic: channel opening, routing, HTLC management, etc. But **no** private keys for signing are stored here.
{% endstep %}

{% step %}
### Remote Validating Signer

Stores private keys in a secure environment and **validates** each request (e.g., channel updates, HTLC commitments) before generating a signature. If the request fails policy checks, it denies signing.
{% endstep %}
{% endstepper %}

**Additional Components**

* **Policy Engine**: A customizable set of rules ensuring no suspicious or off-protocol requests are signed.
* **UTXO Oracle (Optional)**: The signer can be configured to receive chain data to detect remote breaches or track on-chain states (e.g., unconfirmed inputs, HTLC expiries).
* **State Storage**: Provides secure, redundant cloud storage for Lightning nodes and signers with anti-rollback protection.

## Architecture Overview

Below is a simplified technical breakdown of how VLS integrates with Lightning nodes:

{% stepper %}
{% step %}
### Integration Points

* **RGB LN  Node**
{% endstep %}

{% step %}
### Validation Flow

1. **Node** proposes a transaction or state update.
2. **VLS** checks protocol correctness and local policy (e.g., channel open, HTLC amounts, no double revoke).
3. **If valid**, the signer returns a signature. Otherwise, it rejects the request.
{% endstep %}

{% step %}
### Hardware vs. Software Deployment

* VLS can run in a dedicated hardware security module (HSM), a secure enclave, or simply as a separate process/container.
* For extremely large LN balances, hardware isolation is recommended.
{% endstep %}

{% step %}
### Performance & Scalability

* Rust ensures efficient, safe concurrency.
* The overhead for real-time transaction signing is minimal compared to typical LN operations.
{% endstep %}
{% endstepper %}

## Current Status

Support for a **remote signer** in the RGB Lightning Node is currently **under active development**.

The goal of this feature is to allow Lightning and RGB operations to be executed while keeping private keys **outside** of the RGB Lightning Node process. This enables stronger security models such as:

* hardware-backed signing
* isolated signing services
* custodial or enterprise-grade deployments
* integration with external signing infrastructure

At this stage, remote signer support is **not yet available in production** and should be considered experimental.

Progress and technical discussion are tracked publicly here:\
👉 [https://github.com/RGB-Tools/rgb-lightning-node/issues/43](https://github.com/RGB-Tools/rgb-lightning-node/issues/43)

## Next Steps / Further Resources

1. **Policy & Security Deep Dive**
   * https://vls.tech/docs/v0.14.0/security/policy-controls/
   * Understand the specific policy rules that protect channel funds from typical LN exploits.
2. **Sequence Diagrams & Protocol**
   * https://vls.tech/docs/v0.14.0/seq-diagrams/ show how VLS signs off at each step of the LN life cycle.
3. **Contributing / Reporting Issues**
   * We welcome contributors! Check out our https://gitlab.com/lightning-signer/validating-lightning-signer/ or open an issue.
   * Need help? Drop in on our Matrix channel: https://matrix.to/#/#vls-general:matrix.org.
