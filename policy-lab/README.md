# CST8919 Azure Policy Lab

## Overview

This lab is about using Azure Policy to control how resources are created in Azure.

For the MapleTech Solutions scenario, I created three custom policies:

- Only allow resources in West US 3
- Require a `ProjectName` tag
- Deny Public IP addresses

I added the three policies into one initiative called `MapleTech Secure Foundation` and assigned it to my test resource group.

The original lab used Canada Central, but my Azure for Students subscription did not allow me to create the required resources in that region. I used West US 3 instead. The policy logic and test goals stayed the same.

## Demo Video

[Demo](https://youtu.be/coCJBQiVJdc)

## Policies

### Only-WestUS3

This policy denies resources deployed outside West US 3.

### Require-ProjectName-Tag

This policy requires supported resources to have a tag named `ProjectName`.

The tag value can be different, but the `ProjectName` key must exist.

Example:

```text
ProjectName = PolicyLab
```

### Deny-Public-IP

This policy blocks the creation of Public IP address resources.

Resource type:

```text
Microsoft.Network/publicIPAddresses
```

All three policies use the `deny` effect.

## Policy Initiative

The three policies were added to this initiative:

```text
MapleTech Secure Foundation
```

The initiative was assigned to this test resource group:

```text
8919PolicyLab
```

Policy enforcement was set to `Default`, so the deny rules were active.

## Challenges

One challenge was the region restriction on my Azure for Students subscription. I could not use Canada Central, so I changed the approved region to West US 3.

Another challenge was testing one policy at a time. For example, when testing the Public IP policy, I still needed to use West US 3 and add the `ProjectName` tag. Otherwise, more than one policy could block the deployment.

Azure Policy assignments also needed some time before the rules started working.

## What I Learned

I learned that Azure Policy can stop non-compliant resources before they are created.

I also learned that an initiative makes it easier to manage and assign several policies together.

In a real project, more policies could be added for naming rules, allowed VM sizes, encryption, diagnostic settings, and private networking.

## Repository Structure

```text
policy-lab/
├── README.md
├── policy-definitions/
│   ├── Only-WestUS3.json
│   ├── Require-ProjectName-Tag.json
│   └── Deny-Public-IP.json
└── screenshots/
```

