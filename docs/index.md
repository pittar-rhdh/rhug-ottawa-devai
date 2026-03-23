# RHUG Ottawa Planning:  March 25, 2026

## Andrew's Demo:  Enable Develoepr AI with Guardrails and Standardization

This demo helps to highlight the role that *Platform Engineering* plays in enabling developers in large organization (such as Government Departments, Agencies and Crown Corporations) to quickly, safely and cost effectively leverage AI in their day-to-day work.  This demo will cover:

* **Red Hat Developer Hub:** How Golden Path Templates enable standardized access to AI resources embedded in their applications and enabled in their IDEs.
* **OpenShift Dev Spaces:** Standardized, safe, cost effective; Fast and easy developer onboarding with "IDE as Code" using minimal resources only when developers are actually developing.
* **AI Enabled Development:** AI Code Assitants with Guard Rails; Developers are automatically "AI Enabled" with the tools supported by their organization.

## Setup

This demo builds on top of the [Red Hat Trusted Application Pipeline Demo](https://catalog.demo.redhat.com/catalog?item=babylon-catalog-prod/enterprise.redhat-tap-demo.prod&utm_source=webapp&utm_medium=share-link).  So start by ordering an instance for yourself.

Once the demo environment is running, the following modifications and additions will be made.

## Getting Started

Login to the cluster Argo CD instance with the OpenShift "admin" user/pass. Disable autosync for Dev Spaces.

```
https://argocd-server-openshift-gitops.apps.<clusterurl>.opentlc.com/
```

Check your "checluster" resource.  If it isnt' configured to use `https://open-vsc.org` for the plugin registry, then run the following command:

```
oc patch checluster devspaces \
  -n openshift-devspaces \
  --type='merge' \
  -p '{"spec":{"components":{"pluginRegistry":{"openVSXURL":"https://open-vsx.org"}}}}'
```

This will be needed in order to get certain extensions.

## Important Locations

The TSSC software templates are in GitLob at this location:

```
https://gitlab-gitlab.apps.<clusterurl>.opentlc.com/rhdh/trusted-application-pipeline-templates
```

You'll also need to login using the OpenShift CLI to make some changes to the cluster.

### Gemini / Claude API Key Secrets

If you plan on using Gemini with Roo Code or the Claude extension, then you will need to include a secret in the `openshift-devspaces` workspace with these values.

You can see a sample **Claude** API key in the `demo/secrets/claude` director in the root of this repo.

Create your own claude secret with your API key and apply it in the `openshift-devspaces` directory.  For me, that looks like:

```
oc apply -f ignored/secrets/claude-api-key.yaml
```

## Update Software Templates

Next, update the Quarkus software template.  To do this, you'll need to clone the repo first:

```
git clone https://gitlab-gitlab.apps.<clusterurl>.opentlc.com/rhdh/trusted-application-pipeline-templates
```

When you commit/push changes, I simply used `user1`/`<demopassword>`.

Update `scaffolder-templates/quarkus-stssc-template/skeleton/.vscode/extensions.json`. It should look like:

```
{
    // See https://go.microsoft.com/fwlink/?LinkId=827846
    // for the documentation about the extensions.json format
    "recommendations": [
      "redhat.java",
      "vscjava.vscode-java-debug",
      "vscjava.vscode-java-test",
      "redhat.vscode-quarkus",
      "redhat.vscode-yaml",
      "redhat.vscode-openshift-connector",
      "redhat.fabric8-analytics",
      "RooVeterinaryInc.roo-cline",
      "Anthropic.claude-code",
      "Continue.continue"
    ]
}
```

This will add Roo Code, Continue, and Claude.