# RHUG Ottawa Planning:  March 25, 2026

## Andrew's Demo:  Enable Develoepr AI with Guardrails and Standardization

This demo helps to highlight the role that *Platform Engineering* plays in enabling developers in large organization (such as Government Departments, Agencies and Crown Corporations) to quickly, safely and cost effectively leverage AI in their day-to-day work.  This demo will cover:

* **Red Hat Developer Hub:** How Golden Path Templates enable standardized access to AI resources embedded in their applications and enabled in their IDEs.
* **OpenShift Dev Spaces:** Standardized, safe, cost effective; Fast and easy developer onboarding with "IDE as Code" using minimal resources only when developers are actually developing.
* **AI Enabled Development:** AI Code Assitants with Guard Rails; Developers are automatically "AI Enabled" with the tools supported by their organization.

## Setup

This demo builds on top of the [Red Hat Trusted Application Pipeline Demo](https://catalog.demo.redhat.com/catalog?item=babylon-catalog-prod/enterprise.redhat-tap-demo.prod&utm_source=webapp&utm_medium=share-link).  So start by ordering an instance for yourself.

Once the demo environment is running, the following modifications and additions will be made.

### Gemini / Claude API Key Secrets

If you plan on using Gemini with Roo Code or the Claude extension, then you will need to include a secret in the `openshift-devspaces` workspace with these values.