---
title: "Aqua Security Data Processing"
slug: "aqua-security-data-processing"
date: "2022-07-27T15:26:17.591Z"
lastmod: "2024-10-07T09:12:20.386Z"
weight: 2
draft: false
---

# Overview

Aqua Security makes extensive efforts to safeguard your data, and to maintain its confidentiality, privacy, integrity, and availability. The present document describes how Aqua Platform software and Aqua Security ("Aqua") process your data in accordance with these objectives. It covers data collection, transmission, and storage, as well as the related processes and policies. As Aqua Platform continues to evolve and include new capabilities, we will update our policies and processes, and update this document to reflect these changes.

# Legal implications

This document is provided as a supplement to all other Aqua-provided legal documents. It is not intended to supersede or modify legal documents in any way.

# Compliance certifications

Aqua is ISO 27001 and SOC 2 Type II certified. We undergo annual recertification and pen testing by an accredited third-party provider. To learn more about these certifications, please see [Compliance at Aqua](https://www.aquasec.com/trust/compliance/).

# How Aqua handles your data

## Data collection, encryption, transmission, and storage

Aqua collects, transmits, and stores only the data that is necessary to provide and support its products and services for our Customers. All data that is collected is encrypted in every phase of transmission (e.g., from users to servers, and servers to databases) and while at rest (e.g., in databases, Amazon S3 cloud object storage).

## Data residency

Aqua Platform SaaS Edition is deployed in multiple regions around the world. Each region operates as an independent instance of Aqua Platform, with all Customer data remaining physically in that region. Aqua provides you with the option to pre-select the region of your deployment; this may help you comply with cross-border personal data transfers and other legal requirements (such as the GDPR and similar privacy laws) you may be subject to. For more information, see <a>SaaS Regions</a>.

## Data deletion

Data that is not required by Aqua is disposed of quickly. For example: When performing cloud security scans, some API responses contain data that is not used by the scan; this data is simply an artifact of how cloud-provider APIs work. Aqua processes the scan data, saves only what is relevant to the scan, and permanently deletes the remaining data within 36 hours.

## Telemetry

Aqua Platform uses telemetry to transmit selected information to Aqua-managed computing environments. This is required to support various operations, including problem resolution. As with all other data, telemetry data is protected as described.

## Billing data

If you pay Aqua via credit card, your payment information will not be processed, saved, or even seen by us. Aqua uses Stripe, a third-party, PCI-compliant, accredited payment processor, to handle all billing information. Stripe's comprehensive privacy and security policies and information can be viewed [here](https://stripe.com/privacy).

## Activity logging and auditing

Aqua Platform logs all activity related to your account. This includes actions performed by your users (administrators and others) and by Aqua administrators, whether performed via the UI or by using product APIs. The most recent 250 GB of audit data is readily available for retrieval through the UI and log APIs.

Beyond this threshold, audit data is securely archived in long-term storage for up to 365 days. Customers can request access to their archived data by contacting their Customer Success representative.

## The right to be forgotten

You can close your account at any time. Once you have done so, Aqua will stop collecting and transmitting data as described above, and stop logging activity related to your account.

If you want us to delete your data within a specific timeframe, please contact Aqua Support to request a full data wipe. Otherwise, your data will be deleted during a regularly scheduled period (typically within 48 hours).

Please note, however, that we may still retain certain personal data, such as data which we are required to retain to comply with legal obligations to which we are subject, to exercise and defend from legal claims, to perform accounting and billing, and for similar legitimate purposes.

# Data shared with Aqua

This section lists the kinds of data that are shared with Aqua when you use specific Aqua Platform functionality or components.

## Supply Chain Security

Aqua Platform supports two deployment models:

* Remote access: You provide Aqua remote read-only access to your source code repositories. Aqua pulls your code to its infrastructure for the duration of the scan only, and then removes it. Your code is never kept.
* Local access: You deploy the Aqua supply chain broker locally in your private environment. Your code is never sent to Aqua. The data shared with Aqua includes metadata and security findings.

## CSPM and Inventory

Data shared with Aqua includes:

* Read-only connection details for cloud provider accounts, such as AWS (Amazon Web Services), Microsoft Azure, and GCP (Google Cloud Platform) 
* Cloud asset configuration metadata (but not the details of the contents within the cloud resources)
* (If used) Cloud provider event streams, such as AWS CloudTrail, and Azure Activity log

## Image registry and image scanning

Data shared with Aqua includes container image metadata and security findings discovered by the Aqua Scanner. For every image scanned, Aqua receives the following data for use in querying Aqua's security threat database:

* Aqua image digest
* Image operating system
* List of layer digests in the image
* List of packages installed in the image, including:
 * Package format (e.g., rpm, deb, apk)
 * Package name (e.g., nginx)
 * Package version
 * Package hash (if applicable)
* List of non-package executables, including:
  * Name of software
  * Version
  * CPE
  * SHA1 hashes of file contents, for purposes of malware identification
* List of programming-related files (e.g., php, js, jar), and SHA1 hashes of file contents

Aqua Platform supports two deployment models:

* Remote access: You provide Aqua remote access to your registry. Aqua will pull and scan your container images from its own computing infrastructure. Aqua has read-only access to your container images, and stores this information in its infrastructure for the duration of the scan. Data shared with Aqua includes connection parameters for your registries (e.g., Amazon ECR, Azure ACR, or Google GCR).
* Local access: You deploy the Aqua Scanner locally in your private environment. Your images are never sent to Aqua. The data shared with Aqua includes metadata and security findings.

## Workload Protection

This data is shared with Aqua:

* Runtime audit trail and incident information
* Runtime indications (evidence) of security compromises, such as copying files infected with malware
* Audit events include:
 * Host address 
 * Container address
 * Image name
 * Username
 * IP/DNS address (when relevant)
 * User commands (when relevant)
 * Process ID and name
 * Malware name (when relevant)
 * (If Aqua is integrated with secret key stores) Encrypted secrets. If an external vault is used, Aqua will keep only the secret keys, not their values. Enforcers keep the authentication tokens to the Server encrypted on the workload.

## Kubernetes security

The KubeEnforcer is the platform component responsible for Kubernetes security. KubeEnforcers run as Deployments on the clusters to be protected. Security capabilities are implemented at the cluster level without sending the full raw data (the resource manifest) to Aqua. The following data is sent to Aqua:

* List of Kubernetes resources:
 * ConfigMaps
 * CronJobs
 * DaemonSets
 * Deployments
 * Jobs
 * Pods
 * Roles
 * Service Accounts
 * StatefulSets
* Security findings for these resources 
* Metadata of these resources:
 * Resource name
 * Resource type
 * Namespace
 * Number of pods
 * AWS IAM ARN (if present in a role)

A KubeEnforcer Auto-Discovery setting, “Add discovered registries”, allows Aqua to read Kubernetes secrets that hold container registry credentials (“secret docker-registry”) and send this data to Aqua for integration with the registries. This allows Aqua to scan container images directly from the registries. This setting is disabled by default.

## Account Management

Data shared with Aqua includes:

* User email addresses and hashed passwords
* (If used) SAML configuration data for SSO login
* IP addresses and user agents of users connecting to the SaaS interface or APIs

# Sub-processors

Aqua uses sub-processors only for the SaaS Edition; not the Self-Hosted Edition.

# Access to Customer environments

The Customer agrees and consents to Aqua accessing the Customer’s systems solely for the purpose of resolving errors.
