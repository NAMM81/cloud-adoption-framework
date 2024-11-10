---
title: DevSecOps controls
description: Learn about DevSecOps controls and how to integrate security processes and tools into the DevOps development cycle.
author: texnokot
ms.author: martinek
ms.date: 05/20/2024
ms.topic: conceptual
ms.custom: internal
ms.reviewer: ridive, mas, jamesduncan, stbosted, nobiwan, thomq
---
# DevSecOps controls

This article describes how to apply security controls to support the [Continuous SDL](https://www.microsoft.com/SDL) security practices. These security controls are an integral part of a [DevSecOps strategy](/azure/cloud-adoption-framework/secure/innovation-security) spanning people, process, and technology.
This documentation describes each control and shows how to apply these controls to three security profiles. These profiles meet typical security requirements for common business scenarios at most organizations:

:::image type="content" source="media/devsecops-controls/security-control-profiles.png" alt-text="Diagram of security controls versus time and impact.":::

## Security control profiles

There are three tiers of control profiles referenced in this article.

:::row:::
   :::column span="":::
      :::image type="icon" source="media/devsecops-controls/minimum.png" border="false":::
   :::column-end:::
   :::column span="3":::
      **Temporary minimum** – Abbreviated security profile for a **temporary exception state** to support rapid prototyping of low-risk workloads. This profile should be used only for temporary exceptions that need to be released on an accelerated timeline to meet critical business needs. Items using this profile should rapidly be brought up to the standard profile.
   :::column-end:::
:::row-end:::
:::row:::
   :::column span="":::
      :::image type="icon" source="media/devsecops-controls/balanced.png" border="false":::
   :::column-end:::
   :::column span="3":::
      **Standard** - Balanced approach for most workloads, most of the time.
   :::column-end:::
:::row-end:::
:::row:::
   :::column span="":::
      :::image type="icon" source="media/devsecops-controls/high.png" border="false":::
   :::column-end:::
   :::column span="3":::
      **High security** – Stringent security for workloads with a potential high impact on business and human safety.
   :::column-end:::
:::row-end:::

## DevSecOps security controls

This section provides a reference of recommended security controls for each type of workload. This reference might be adopted as is or it can be adapted to your existing software development and software security processes. Most organizations can’t implement all these controls right away if they aren’t already doing some of them. Taking a continuous improvement approach is often the best approach: prioritize controls, implement the first control, move to the next control, implement it, and so on. Most organizations should prioritize the [critical foundations](#establish-critical-foundations) first.

For more information, see [The DevSecOps journey](innovation-security.md).

:::image type="content" source="media/devsecops-controls/devsecops-security-profile-comparison.png" alt-text="This diagram summarizes the security controls and how to apply them to each workload security profile." lightbox="media/devsecops-controls/devsecops-security-profile-comparison.png":::

Key planning considerations include:

- **Shift left… but double-check** - This reference is designed to detect and correct issues as early as possible to enable you to fix them when it's easier and cheaper to fix the issues (sometimes called shift left), but also to assume failure and include double-checking later in the process. Always double-check any security controls in the CI/CD process, ensure avoidable issues don’t slip through to production systems. This concept follows "defense in depth" and "fail safe" principles.
- **Artificial Intelligence (AI)** – The two main implications of artificial intelligence are:
   - **Secure all code** regardless of whether written by human or generative AI
   - **Use both for security** - Apply both classic and AI controls as available to increase visibility and context for any security issues (such as code analysis tools)

## Security controls

The controls are grouped into the stages of development they apply to and the common controls (critical foundations) that apply across all development stages and control profiles:

- **[Critical foundations](#establish-critical-foundations)**
   - [Provide security training](#providing-security-training)
   - [Security in blameless postmortems](#include-security-in-blameless-postmortems)
   - [Secure coding standards](#establish-security-standards-metrics-and-governance)
   - [Tool chain security](#require-use-of-proven-security-features-languages-and-frameworks)
   - [Secure identities](#foundational-identity-security)
   - [Strong cryptographic standards](#cryptographic-standards)
   - [Secure development environment](#securing-your-development-environment)
- **[Secure design](#secure-design)**
   - [Threat model (security design review)](#perform-threat-modeling-security-design-review)
- **[Secure code](#secure-code)**
   - [Code analysis](#code-analysis)
- **[Secure CI/CD pipeline](#secure-the-cicd-pipeline)**
   - [Reinforce/check secure the code controls](#supply-chain--dependency-management)
   - [Security code review](#security-code-review)
   - [Credential and secret scanning](#credential-and-secret-scanning)
   - [Secure pipeline (access/infrastructure/apps)](#secure-pipeline)
- **[Secure operations](#secure-operations)**
   - [Live site penetration testing](#live-site-penetration-testing)
   - [Identity/application access and controls](#identityapplication-access-controls)
   - [Host/container controls](#hostcontainerenvironment-controls)
   - [Network access controls](#network-access-controls)
   - [Monitoring, response, and recovery](#monitoring-response-and-recovery)

Each of these items is defined in the following sections:

### Establish critical foundations

This control supports Continuous SDL Practice 1 – Establish security standards, metrics, and governance, Practice 2 – Require use of proven security features, languages, and frameworks, and Practice 10 – Provide security training.

:::row:::
   :::column span="":::
      :::image type="icon" source="media/devsecops-controls/balanced.png" border="false":::
   :::column-end:::
   :::column span="3":::
      **Standard** - These controls apply across all development stages and control profiles.
   :::column-end:::
:::row-end:::

#### Providing security training

This control focuses on providing your developers and security teams with training to recognize and resolve security issues through the development lifecycle. Without security training your teams could miss core security weaknesses that lead to compromise during the applications lifetime.

As a result, it's imperative that you implement security training across all roles (including users, developers, product line managers, testers, and more). Each role must have education on security risks and their role in keeping applications safe. This training might take the form of: formal or on-demand training, simulation exercises, threat modeling, mentoring/advisors, security champions, application security support teams, purple team activities, podcasts, videos, or any other learning methods.

Ultimately, each role needs to understand: 

- Why it’s important to address security risks
- What they need to do for security in their role
- How to make security part of their everyday role

People who understand the attacker’s perspective, their goals, and how that shows up in real world security incidents quickly become security allies instead of trying to avoid security.

Security is a never-ending game where the threats, technology, and business assets to protect are always changing and the threat actors never give up. Security training approach must be ongoing and continuously evolve. Effective training aligns with and reinforces security policies, software development lifecycle (SDL) practices, standards, and software security requirements. Training material should come from insights derived from data and newly available technical capabilities.

Although security is everyone’s job, it’s important to remember that not everyone needs to be a security expert nor strive to become a proficient penetration tester. Ensuring everyone understands security basics and how to apply them to their role of building security into software and services is essential. This training should include the safe use of workstations, applications, identity, and accounts.

In particular, developers and the engineers building systems aren't usually security experts. Training in both the technical and conceptual aspects of threat modeling is necessary for them to become effective so they can build systems that are secure by design. This training is vital for the threat modeling process to work at-scale in organizations where developers far outnumber security professionals. Threat modeling must be thought of as a fundamental engineering skill in which all developers and engineers must have at least basic proficiency. Therefore, development and engineering teams must be trained to be competent at threat modeling as part of onboarding and with periodic refreshers.

#### Include security in blameless postmortems

Blameless postmortem analysis is a critically important method for teams to learn from mistakes effectively and efficiently without triggering defensiveness from team members by seeking someone to blame. Security learnings should be explicitly included into the blameless postmortem process to ensure the teams are also maximizing security learnings.

#### Establish security standards, metrics, and governance

Organizations should establish these security standards, metrics, and governance because they underpin the ability to innovate. It enables a strong security program that not only protects the organization’s assets but also aligns with its business objectives. Security standards are the baseline requirements and best practices for keeping an organization's systems, data, and process safe.

These standards should be measured and governed, including monitoring for compliance and regularly reviewing and updating them for current threats, tooling, and other factors. This process should cover the entire lifecycle from initial ideation through the decommissioning of the application and any supporting development environments.

Metrics are measurements used to see how effective the security controls and processes are. One key metric is the Mean Time To Remediate (MTTR) for tracking how long an application remains vulnerable. This measurement allows us to strategically invest in issuing security fixes more promptly. 

> [!NOTE]
> This concept differs from MTTR in security operations focused on time to remove adversary access to the organization’s assets.

Security governance acts as a guiding hand to security teams and are often built upon frameworks and processes that organizations use to manage and control their information security. This guidance includes Policies, Procedures, Controls, and Risk Management. Metrics help quantify risk exposure. Without them, the organization might not fully understand its vulnerabilities and potential impact.

Because security requirements might be new, you have the opportunity to take a progressive approach that gradually ramps up coding standards to the ideal state. This approach gives teams time to learn and automate the monitoring and controls.

#### Require use of proven security features, languages, and frameworks

Define and publish a list of approved tools and their associated security checks. Using well-established and proven security solutions is important to avoid common mistakes because building secure solutions is very challenging. Attempting to reinvent security solutions almost always results in increased security risk and wasted time and effort.

Ensure developers and engineers are taking advantage of new security analysis functionality and protections. They should always use the latest compiler, linker, libraries, and the appropriate compiler and linker flags to generate secure executables.

Organizations should implement a review and approval process to validate the security of any integrated components. They should establish a policy to only use approved components in build and deploy processes that are enforced and monitored.

#### Foundational identity security

Ensure that the use and integration of identity follows well-established security best practices. Threat actors use identity attack techniques frequently against both production systems and development processes. A popular saying captures this, "attackers don't break in, they just log in."

Identity security takes two forms for development:

- Identity Security for Development Process - Ensure that all participants in the development process use strong authentication methods for their daily work and only have privileges required to execute their job tasks. For more information, see the section [Identity/application access controls](#identityapplication-access-controls).
- Identity Security for Systems and Applications - Ensure that the systems they're designing and building follow best practices for authentication and authorization methods (and aren’t building their own weak imitations of proven and maintained identity systems).

Apply identity security for systems and applications by following the guidance in these resources:

- [Secure your organization's identities with Microsoft Entra](/entra/fundamentals/concept-secure-remote-workers)
- [Microsoft identity platform](/entra/identity-platform/)
- [What is the Microsoft identity platform?](/entra/identity-platform/v2-overview)

#### Cryptographic Standards

Apply sound cryptographic practices to all usage of cryptography. Follow all the guidelines described in Continuous SDL Practice 4 – Define and Use cryptographic Standards.

For more information, see [Microsoft SDL cryptographic recommendations](/security/engineering/cryptographic-recommendations).

#### Securing your development environment

This control supports Continuous SDL Practice 6 – Securing your engineering environment.

This control focuses on securing your development environment using secure workstations and Integrated Development Environments (IDEs). This control highlights the benefit of using a Zero Trust approach in your software development lifecycle.

In the current landscape, attackers expand their operations to target your developers’ machines and tamper with build processes. A pivotal example of this attack was the one experienced by SolarWinds, where the attacker inserted a malicious DLL before the final stages of the software build. Effectively this backdoored the application and resulted in a targeted attack that was distributed to thousands of customers worldwide via the supply chain. For more information about the SolarWinds attack, see the Microsoft Blog [Analyzing Solorigate, the compromised DLL file that started a sophisticated cyberattack, and how Microsoft Defender helps protect customers](https://www.microsoft.com/security/blog/2020/12/18/analyzing-solorigate-the-compromised-dll-file-that-started-a-sophisticated-cyberattack-and-how-microsoft-defender-helps-protect/).

It's essential to harden workstations, build environments, identities, and other development systems to ensure the integrity of developed applications. Failure to do so creates a pathway for attackers to compromise your application via your Source Code Management (SCM) system or via your developer workstation.

This practice is a critical foundation of your development lifecycle and should be established over all profiles.

Throughout this practice, you must take a Zero Trust approach. At its core the [Zero Trust model](https://www.microsoft.com/security/business/zero-trust) requires that each access request (user, service, or device) is verified as though it originated from an untrusted network, regardless of where the request originates or what resource it accesses. Base this "always authenticate and authorize" policy on all available data points. You should limit user access, especially privileged users, through Just-In-Time and Just-Enough-Access (JIT/JEA) policies, and segment access to minimize the possible damage if there's a breach. 

Hardening your development environment can be achieved through various methods, however a good starting point is to consider the developer workstation. By utilizing technologies such as [GitHub Codespaces](https://docs.github.com/codespaces/overview) or [Microsoft DevBox](/azure/dev-box/overview-what-is-microsoft-dev-box), you shift the development environment to SaaS applications, which can then be managed through security and network settings or through organizational policies.

To further lockdown developer workstations, you can issue them privileged access workstations/secure access workstations (PAW/SAW). These workstations help you reduce threat vectors and ensure a standardized and controlled developer device.

- [Why are privileged access devices important](/security/privileged-access-workstations/privileged-access-devices)
- [Deploying a privileged access solution](/security/privileged-access-workstations/privileged-access-deployment)

### Secure design

#### Perform threat modeling (security design review)

This control supports Continuous SDL Practice 3 – Perform Threat Modeling.

This control identifies security weaknesses in the design that can result in security incidents and business damage. Security weaknesses in the design can be difficult to mitigate after the design is implemented, so finding and fixing these weaknesses early in the lifecycle is critically important.

Threat modeling serves as the security design review process, which integrates security into the design of a system or application.

Threat modeling systematically identifies, assesses, prioritizes, and mitigates security risks within a software system. This structured approach to analyzing the design and architecture of a software application identifies potential threats and vulnerabilities early in the development process.

The ultimate goal is to understand the system and what could go wrong. Threat modeling helps achieve that goal by applying a deep understanding of both the system itself and how a potential attacker views it.

This process typically takes the form of threat discovery workshops where a team of experts on the system and security experts work together to discover and document risks. While this process might start informally, it should quickly evolve into a structured process that discusses each aspect of the service being built, how it's used, and system interfaces.

The stages of threat modeling are:

- **Identify use cases, scenarios, and assets** – Start with understanding what business functions and use cases the system enables to help assess the potential business impact of any system compromise and inform the discussions to follow.
- **Create an architectural overview** – Create a visual summary of the application (or use an existing one) to provide a clear understanding of the system and how it works. This overview should include: a business process map, components and subsystems, trust boundaries, authentication and authorization mechanisms, external and internal interfaces, and data flows between actors and components.
- **Identify the threats** - Use a common methodology for enumerating potential security threats such as the [STRIDE model](/azure/security/develop/threat-modeling-tool-threats) or [OWASP threat modeling](https://owasp.org/www-community/Threat_Modeling).
- **Identify and track mitigations** - Monitor and track discovered design flaws using existing development processes and tools to ensure the fixes are implemented and documented. This process should include, prioritizing which mitigations to do first so that teams spend their time on the most important efforts first. This process is risk driven and you might not have resources to fully mitigate all risks in the first cycle. Carefully consider which mitigations, including partial mitigations, raise the cost for an attacker for the least defensive cost and resources. The goal of security is attacker failure, which can take the form of fully blocking an attack technique, detecting them to enable a response, slowing them down to give security time to respond, limiting the scope of damage, and more.

A threat model often serves as an education process for all involved as well as providing important context for other security planning, implementation, and testing.

Applications that include the use of Artificial Intelligence (AI) components must evaluate the specific risk types associated with AI, which are different from classic applications.

- [Threat Modeling Security Fundamentals learning path](/training/paths/tm-threat-modeling-fundamentals/)
- [Microsoft Threat Modeling Tool](https://www.microsoft.com/download/details.aspx?id=49168)

Create and analyze threat models by: communicating about the security design of their systems, analyzing those designs for potential security issues using a proven methodology, and suggesting and managing mitigations for security issues.

- [Threat Modeling AI/ML Systems and Dependencies](/security/engineering/threat-modeling-aiml)
- [Integrated threat modeling with DevOps](/security/engineering/threat-modeling-with-dev-ops)

### Secure code

#### Code analysis

This control supports Continuous SDL Practice 7 – Perform Security Testing.

This control focuses on increasing the security of the code as developers write/enter it into an integrated development environment (IDE) or as they check in code. This control is the cornerstone of DevSecOps practices as it directly addresses vulnerabilities that attackers exploit regularly.

Without this control, you might be missing vulnerabilities that are coded directly into your application by your developers. Your developers aren't being malicious but might lack the skilling needed to identify why what they coded is insecure.

This control is key to get the productivity and security benefits of a shift left approach by integrating tools directly into the IDE. This process enables quick discovery and remediation of vulnerabilities at the earliest and most cost effective opportunity. This process can be retroactively applied to already developed applications by identifying security weaknesses and fixing them later (though at greater expense and difficulty).

This process typically takes the form of IDE plug-ins or dedicated scanning tools that scan the code using Static Analysis Security Testing (SAST) and Dynamic Analysis Security Testing (DAST) toolsets.

SAST tools scan the existing codebase and have full access to the code. SAST tools can identify core weaknesses in the code itself. DAST on the other hand is executed on the deployed application. As a result, it has no access to the code and is executed to simulate and identify security weaknesses in runtime.

> [!NOTE]
> AI applications have different types of vulnerabilities (like biases and hallucinations) than classic applications and require tools that focus on those.

**Quality control matters!** A key consideration for running these tools is ensuring that you're tuning them to reduce the noise and wasted effort from false positives. Tuning these tools typically requires a security professional with a developer background that understands your organization’s development processes. The same professionals can also provide triage guidance and expertise on individual detections for developers. They can help distinguish true and false positives, real issues vs. false alarms. The processes for developers to access these experts is often closely related to [Providing Security Training](#providing-security-training) such as through champions programs, application security support teams, etc.

:::row:::
   :::column span="":::
      :::image type="icon" source="media/devsecops-controls/minimum.png" border="false":::
   :::column-end:::
   :::column span="3":::
      **Temporary minimum** – Ensure you enable built-in IDE security features and implement a minimum level of SAST Scanning across your repository to identify vulnerabilities across the application. There must be a documented process to remediate discovered issues in a reasonable time, though the "bug bar" standard of which flaws must be fixed is limited until the application reaches the standard balanced or high security profiles.
   :::column-end:::
:::row-end:::
:::row:::
   :::column span="":::
      :::image type="icon" source="media/devsecops-controls/balanced.png" border="false":::
   :::column-end:::
   :::column span="3":::
      **Standard** - Ensure you fully scan all components with all applicable SAST/DAST tooling and identify weaknesses. Ensure full security coverage over your application code. Ensure you're following the documented process for remediation and have a "bug bar" standard that matches your organization’s risk tolerance.
   :::column-end:::
:::row-end:::
:::row:::
   :::column span="":::
      :::image type="icon" source="media/devsecops-controls/high.png" border="false":::
   :::column-end:::
   :::column span="3":::
      **High security** – Ensure all applicable applications enforce a detailed and documented process addressing all security vulnerabilities. Enforce fixes before any build or release activities. Ensure you're following the documented process for remediation and have a highly restrictive "bug bar" that matches your organization’s risk tolerance for high security business-critical workloads.
   :::column-end:::
:::row-end:::

There are many tools available to use for static analysis. Review the list at [Microsoft Security Development Lifecycle](https://www.microsoft.com/securityengineering/sdl) to find more information.

### Secure the CI/CD pipeline

#### Supply chain / dependency management

This control supports Continuous SDL Practice 5 - Securing the Software Supply Chain.

This control focuses on securing your development supply chain by using Software Composition Analysis (SCA) tools and frameworks such as the Secure Supply Chain Consumption Framework (S2C2F). These processes help reduce the risk of compromise by non-Microsoft code.

In today’s landscape, most applications rely on open source software (OSS) with little oversight or control from consumers of these components. This control highlights core strategies, techniques, and technologies to securely ingest, consume, use, and maintain OSS. It also emphasizes securing internal dependencies, ensuring a complete end-to-end lifecycle, regardless of who coded the software.

Failure to control your software supply chain exposes you to significant vulnerabilities introduced by code you don't control. A notorious example is the log4J/Log4Shell vulnerability, which allowed remote code execution in any system or application using this package. Such vulnerabilities can arise accidentally or maliciously.

Securing your supply chain is an essential part of ensuring a secure development lifecycle and should be considered at every profile state, although every single state should follow the same standardized process of ingesting dependencies.

:::row:::
   :::column span="":::
      :::image type="icon" source="media/devsecops-controls/minimum.png" border="false":::
   :::column-end:::
   :::column span="3":::
      **Temporary minimum** – Inventory all of your dependences so you understand the impact an OSS vulnerability has on your application. This inventory can be achieved using [Dependabot](https://docs.github.com/code-security/dependabot) or other Software Composition Analysis (SCA) tools. These tools might also help you generate a Software bill of Materials (SBOM).
   :::column-end:::
:::row-end:::
:::row:::
   :::column span="":::
      :::image type="icon" source="media/devsecops-controls/balanced.png" border="false":::
   :::column-end:::
   :::column span="3":::
      **Standard** - Analyze all OSS Vulnerabilities and automatically fix them with automatic pull requests. This control can also be achieved by using [Dependabot](https://docs.github.com/code-security/dependabot) and the GitHub Dependency graph/review.
   :::column-end:::
:::row-end:::
:::row:::
   :::column span="":::
      :::image type="icon" source="media/devsecops-controls/high.png" border="false":::
   :::column-end:::
   :::column span="3":::
      **High security** – Actively block all insecure packages with exploitable vulnerabilities being used in the application.
   :::column-end:::
:::row-end:::

To learn more about this control and measure your OSS Security maturity, review the [OSS Supply Chain Framework](https://www.microsoft.com/securityengineering/opensource) and [GitHub’s best practice documentation on Securing your development lifecycle](https://docs.github.com/code-security/supply-chain-security/end-to-end-supply-chain/end-to-end-supply-chain-overview).

#### Security code review

This control focuses on having a security expert review code to identify potential security flaws. This helps find security issues that are hard to automate detections for.

This review could be performed by: a peer on the same team with application security expertise, a security champion within the organization, an application security expert from central app security team, or an external party.

This review must always be a separate person from the developer who wrote the code. This review should be done as a separate activity after automated code analysis is complete.

:::row:::
   :::column span="":::
      :::image type="icon" source="media/devsecops-controls/minimum.png" border="false":::
   :::column-end:::
   :::column span="3":::
      **Temporary minimum** – This control is recommended for this profile.
   :::column-end:::
:::row-end:::
:::row:::
   :::column span="":::
      :::image type="icon" source="media/devsecops-controls/balanced.png" border="false":::
   :::column-end:::
   :::column span="3":::
      **Standard** - This control is recommended for this profile.
   :::column-end:::
:::row-end:::
:::row:::
   :::column span="":::
      :::image type="icon" source="media/devsecops-controls/high.png" border="false":::
   :::column-end:::
   :::column span="3":::
      **High security** – This control is required for all high security applications and often involves multiple individual experts.
   :::column-end:::
:::row-end:::

#### Credential and secret scanning

This control supports Continuous SDL Practice 7 – Perform Security Testing.

This control focuses on reducing risk from authentication keys and other secrets exposed in code. Threat actors have expertise and automation to find and exploit embedded secrets in code.

The best approach is to use managed identities and modern authentication protocols instead of keys and secrets when possible. While using API keys and secrets have traditionally been a coding and testing practice, the preferred method should always be identity-based authentication to resources because of the increased security and lifecycle management abilities. The implementation of this control takes the form of using managed identities, like [Managed identities for Azure resources](/entra/identity/managed-identities-azure-resources/overview).

If the use of secrets is required, you must secure them through their whole lifecycle including their creation, use, regular rotation, and revocation. Avoid directly using secrets in code and only store them in a secure key/secret storage system such as Azure Key Vault or a Hardware Security Module (HSM) if necessary. **Under no circumstances should plain text keys and secrets ever be stored in code, even temporarily!** Attackers find and exploit these secrets.

> [!IMPORTANT]
> Internal source code repositories are not safe!
>
> Internal repositories should be subject to the same requirements as publicly facing repositories as threat actors frequently hunt for secrets and keys in repositories after gaining access to an environment through phishing or other means. This is required for a Zero Trust approach that assumes breach and designs security controls accordingly.

:::row:::
   :::column span="":::
      :::image type="icon" source="media/devsecops-controls/balanced.png" border="false":::
   :::column-end:::
   :::column span="3":::
      **Standard** - Good secret hygiene is essential and is required in all profiles.
   :::column-end:::
:::row-end:::

> [!NOTE]
> As these secrets are found by your teams or by attackers, you must ensure that the key cannot be used to access resources (varies by resource type) in addition to modifying the mechanism to a more secure access method like managed identities.

More details and resources include:

- [Secret Scanning for GitHub Advanced Security for Azure DevOps](/azure/devops/repos/security/github-advanced-security-secret-scanning)
- [Best practices for using Azure Key Vault](/azure/key-vault/general/best-practices)

> [!NOTE]
> We strongly recommend using per workload keys with secret storage solutions like Azure Key Vault.

#### Secure pipeline

This control supports Continuous SDL Practice 5 - Securing the Software Supply Chain.

This control focuses on securing the DevOps pipeline and all the artifacts created during the build processes of your application.

Pipelines are an essential part of automating core repeatable activities within the DevSecOps Lifecycle. In CI/CD, your team merges developer code into a central codebase on a regular schedule and automatically runs standard builds and test processes, which include security toolsets.

Using pipelines to run scripts or deploy code to production environments can introduce unique security challenges. Ensure that your CI/CD pipelines don't become avenues to run malicious code, allow credentials to be stolen, or give attackers any surface area for access. You should also ensure that only the code your team intends to release is deployed. This process includes artifacts of your CI/CD pipelines, especially artifacts that are shared between different tasks that can be used as part of an attack.

**Software Bill of Materials (SBOM)** generation should be automated into the build process to create this critically important code provenance artifact without requiring manual developer actions.

Pipeline security can be assured by ensuring good access control to resources used in pipeline and validating/updating core dependencies/scripts regularly. It's important to note that scripts used in CI/CD pipelines are also code and should be treated in the same way you treat other code in your project.

> [!NOTE]
> The security of the pipeline is dependent on the security of the underlying infrastructure and the accounts/identities that are used for the process. For more information, see the securing your development environment and the secure operations controls (Identity Identity/App Access Controls, Host/Container Controls, Network Access Controls)

:::row:::
   :::column span="":::
      :::image type="icon" source="media/devsecops-controls/balanced.png" border="false":::
   :::column-end:::
   :::column span="3":::
      **Standard** - This control should be evaluated on an access level to every resource in the project; it's a required control across all DevSecOps profile levels.
   :::column-end:::
:::row-end:::

To learn more about pipeline security, see [Securing Azure Pipelines](/azure/devops/pipelines/security/overview).

### Secure operations

#### Live site penetration testing

This control supports Continuous SDL Practice 7 – Perform Security Testing.

Have professional application penetration testers attempt to compromise a live instance of the complete workload. This testing validates that the workload's security controls are effective and consistent. Penetration testing helps find and highlight the path of least resistance that an attacker could use to exploit your application and compromise the business. Penetration tests can be incredibly valuable when done at the right time. Use them after you mitigate the cheap and easy to exploit vulnerabilities found in previous scans.

We recommend you do this testing at all levels of the DevSecOps security profiles.

:::row:::
   :::column span="":::
      :::image type="icon" source="media/devsecops-controls/minimum.png" border="false":::
   :::column-end:::
   :::column span="3":::
      **Temporary minimum** – We recommend that you do a penetration test on all applications. Due to time constraints, you might only be able to identify easier methods into the application that an attacker might exploit. Plan to quickly bring this value up to the standard level at minimum.
   :::column-end:::
:::row-end:::
:::row:::
   :::column span="":::
      :::image type="icon" source="media/devsecops-controls/balanced.png" border="false":::
   :::column-end:::
   :::column span="3":::
      **Standard** - At a standard profile, we recommend that you do a penetration test. In this case, you might uncover more complex vulnerabilities due to the extra care that is taken early in the development process.
   :::column-end:::
:::row-end:::
:::row:::
   :::column span="":::
      :::image type="icon" source="media/devsecops-controls/high.png" border="false":::
   :::column-end:::
   :::column span="3":::
      **High security** – For line of business applications and critical workloads, it’s a requirement to complete a penetration test. Any vulnerability in these applications should be treated with extra attention and care.
   :::column-end:::
:::row-end:::

Integrate the findings and feedback from these activities to improve your security processes and tools.

#### Identity/application access controls

This control supports Continuous SDL Practice 8 – Ensure operational platform security and Practice 6 – Securing your engineering environment.

Ensure that security best practices for identity and access management including [securing privileged access](/security/privileged-access-workstations/overview) are followed for all technical elements of the development environment, CI/CD pipeline, operational workload, and other development systems. Threat actors have sophisticated methods and automation for identity attacks that they use frequently against both production systems and development processes. Identity and access management is a foundational pillar of the [Zero Trust model](https://www.microsoft.com/security/business/zero-trust) that Microsoft recommends.

Ensure security best practices are followed for all development systems and the infrastructure hosting them (VMs, containers, network devices, and more).

:::row:::
   :::column span="":::
      :::image type="icon" source="media/devsecops-controls/minimum.png" border="false":::
   :::column-end:::
   :::column span="3":::
      **Temporary minimum** – Ensure everyone uses multifactor authentication and can only access systems required to perform their daily tasks.
   :::column-end:::
:::row-end:::
:::row:::
   :::column span="":::
      :::image type="icon" source="media/devsecops-controls/balanced.png" border="false":::
   :::column-end:::
   :::column span="3":::
      **Standard** - Ensure that the infrastructure components hosting the workload (such as VMs, containers, network, and identity systems) meet security best practices for identity and access management, including securing privileged access.
   :::column-end:::
:::row-end:::
:::row:::
   :::column span="":::
      :::image type="icon" source="media/devsecops-controls/high.png" border="false":::
   :::column-end:::
   :::column span="3":::
      **High security** – Implement a full Zero Trust strategy that incorporates MFA, Identity Threat Detection and Response, and Cloud Infrastructure Entitlement Management (CIEM). [Perform workload-specific threat model](#perform-threat-modeling-security-design-review) of identity systems and components supporting each high security workload.
   :::column-end:::
:::row-end:::

Managed Identities are the more secure and preferred method of authentication wherever possible. The use of tokens and secrets is less secure due to the need to store and retrieve them at the application layer. In addition, Managed Identities are automatically rolled over without the need for manual intervention.

More details and resources include:

- [Securing Privileged Access (SPA) guidance](/security/privileged-access-workstations/overview)
- [Five steps to securing your identity infrastructure](/azure/security/fundamentals/steps-secure-identity)
- [What are managed identities for Azure resources?](/entra/identity/managed-identities-azure-resources/overview)
- [What is Microsoft Entra Privileged Identity Management](/entra/id-governance/privileged-identity-management/pim-configure)
- [What's Microsoft Entra Permissions Management?](/entra/permissions-management/overview)

#### Host/container/environment controls

This control supports Continuous SDL Practice 8 – Ensure operational platform security and Practice 6 – Securing your engineering environment.

Ensure that security best practices are followed for all compute resources and hosting environments for all technical elements of the development lifecycle. Threat actors have sophisticated methods and automation for infrastructure and user endpoint attacks that they use frequently against both production systems and development processes. Infrastructure security is a foundational pillar of the [Zero Trust model](https://www.microsoft.com/security/business/zero-trust) that Microsoft recommends.

This control must include all elements of the development and operational lifecycle including but not limited to:

- General IT/operational workstations and environments
- Dedicated development workstations and environments
- CI/CD pipeline infrastructure
- Workload hosting environments
- Any other development systems.

This control includes any resource that can run any code including but not limited to:

- Virtual Machine (VM) hosts and VMs
- Containers and container infrastructure
- Application, script, and code hosting platforms
- Cloud subscriptions/accounts and enrollments
- Developer, User, and IT Admin Workstations

Ensure that you apply security best practice to the infrastructure components including security updates (patches), baseline security configurations, and more.

:::row:::
   :::column span="":::
      :::image type="icon" source="media/devsecops-controls/minimum.png" border="false":::
   :::column-end:::
   :::column span="3":::
      **Temporary minimum** – Apply standard enterprise configurations for hosts and subscriptions.
   :::column-end:::
:::row-end:::
:::row:::
   :::column span="":::
      :::image type="icon" source="media/devsecops-controls/balanced.png" border="false":::
   :::column-end:::
   :::column span="3":::
      **Standard** - Ensure that the infrastructure meets security best practices outlined in the Microsoft Cloud Security Benchmark (MCSB).
   :::column-end:::
:::row-end:::
:::row:::
   :::column span="":::
      :::image type="icon" source="media/devsecops-controls/high.png" border="false":::
   :::column-end:::
   :::column span="3":::
      **High security** – Stringently apply MCSB standards and [perform workload-specific threat model](#perform-threat-modeling-security-design-review) of infrastructure supporting each high security workload.
   :::column-end:::
:::row-end:::

More details and resources include:

- [Microsoft Cloud Security Benchmark (MCSB)](/security/benchmark/azure/)
- [Microsoft Defender for Cloud](/azure/defender-for-cloud/)
- [AppLocker](/windows/security/application-security/application-control/windows-defender-application-control/applocker/applocker-overview)
- [Securing SQL Server](/sql/relational-databases/security/securing-sql-server)
- [Windows Security baselines](/windows/security/operating-system-security/device-management/windows-security-configuration-framework/windows-security-baselines)
- [App Control and virtualization-based protection of code integrity](/windows/security/application-security/application-control/introduction-to-virtualization-based-security-and-appcontrol)

#### Network access controls

This control supports Continuous SDL Practice 8 – Ensure operational platform security and Practice 6 – Securing your engineering environment.

Ensure that security best practices for network access management are followed for all technical elements of the development environment, CI/CD pipeline, operational workload environment, and other development systems. Threat actors have sophisticated methods and automation for identity attacks that they use frequently against both production systems and development processes. Network security is a foundational pillar of the [Zero Trust model](https://www.microsoft.com/security/business/zero-trust) that Microsoft recommends.

Network security should include:

- **External Network Protection** – Isolation from unsolicited external/internet traffic and mitigation of known attack types. This isolation typically takes the form of internet firewall, web application firewall (WAF), and API security solutions.
- **Internal Network Protection** – Isolation from unsolicited internal traffic (from other enterprise network locations). This isolation might use similar controls as external network protection and might be granular to the workload or to specific individual components and IP addresses.
- **Denial of Service Mitigations** – Protections against Distributed Denial of Service (DDoS) and other denial of service attacks.
- **Security Service Edge (SSE)** – Use of client side microsegmentation to provide secure access directly to resources, including application of Zero Trust policies.

Ensure security best practices are followed for all development systems and the infrastructure hosting them (VMs, containers, network devices, and more).

:::row:::
   :::column span="":::
      :::image type="icon" source="media/devsecops-controls/minimum.png" border="false":::
   :::column-end:::
   :::column span="3":::
      **Temporary minimum** – Apply standard enterprise configurations for workload.
   :::column-end:::
:::row-end:::
:::row:::
   :::column span="":::
      :::image type="icon" source="media/devsecops-controls/balanced.png" border="false":::
   :::column-end:::
   :::column span="3":::
      **Standard** - Ensure all systems have external network protection, DDoS protection, and a minimum of per-workload internal network protection.
   :::column-end:::
:::row-end:::
:::row:::
   :::column span="":::
      :::image type="icon" source="media/devsecops-controls/high.png" border="false":::
   :::column-end:::
   :::column span="3":::
      **High security** – All standard protections plus high granularity of internal network protections, forced tunneling of outbound server traffic through external network protection mechanisms, and a [workload-specific threat model](#perform-threat-modeling-security-design-review) of network infrastructure supporting each high security workload.
   :::column-end:::
:::row-end:::

More details and resources include:

- [MCSB network security](/security/benchmark/azure/mcsb-network-security)
- [Microsoft Defender for Cloud ](/azure/defender-for-cloud/)
- [Azure Firewall](/azure/firewall/overview)
   - [Azure Firewall forced tunneling](/azure/firewall/forced-tunneling)
   - [Azure Security Baseline for Azure Security Firewall](/security/benchmark/azure/baselines/azure-firewall-security-baseline)
   - [Azure Firewall threat intelligence-based filtering](/azure/firewall/threat-intel)
- [Azure Web Applications Firewalls (WAF)](/azure/web-application-firewall/overview)
- [Azure DDoS Protection](/azure/ddos-protection/ddos-protection-overview)

#### Monitoring, response and recovery

This control supports Continuous SDL Practice 9 – Implement Security Monitoring and Response.

Ensure that security operations (SecOps/SOC) teams have visibility, threat detection, and response procedures for workloads (APIs and apps) as well as the infrastructure hosting them. Ensure that cross-team processes and tooling between SecOps and Infrastructure/Workload teams enables rapid recovery after an attack.

This control sustains the security of the workload once it’s in production and actively running in your organization. This process should be integrated with your existing [security operations](/azure/cloud-adoption-framework/organize/cloud-security-operations-center) capability that detects and responds to security incidents.

Security monitoring for custom workloads combines extended detection and response (XDR) solutions for common components by analyzing logs and other application data to detect and investigate potential security threats. Custom application data often includes: information about user requests, application activity, error codes, network traffic, other relevant details from the application, databases, network endpoints, and other system components.

This data is then enhanced with insights from real-time threat intelligence to identify patterns of anomalous behavior that could indicate potential attempts to infiltrate the network. Once aggregated, correlated, and normalized, the XDR and Security Information and Event Management (SIEM) platform offers remediation actions.

:::row:::
   :::column span="":::
      :::image type="icon" source="media/devsecops-controls/minimum.png" border="false":::
   :::column-end:::
   :::column span="3":::
      **Temporary minimum** – Deploy XDR capabilities in your environment to monitor traffic of your end user devices.
   :::column-end:::
:::row-end:::
:::row:::
   :::column span="":::
      :::image type="icon" source="media/devsecops-controls/balanced.png" border="false":::
   :::column-end:::
   :::column span="3":::
      **Standard** - Deploy XDR and custom SIEM detections that identify anomalous behavior relative to the overall environment. This profile might include custom detections for individual workloads.
   :::column-end:::
:::row-end:::
:::row:::
   :::column span="":::
      :::image type="icon" source="media/devsecops-controls/high.png" border="false":::
   :::column-end:::
   :::column span="3":::
      **High security** – Standard controls plus custom per-workload detections based on insights from threat modeling of the workload. Combine this profile with AI to provide contextual awareness to remediation recommendations.
   :::column-end:::
:::row-end:::

- [Microsoft Defender](/defender)
- [Microsoft Sentinel](/azure/sentinel)
- [Manage and respond to security alerts](/azure/defender-for-cloud/managing-and-responding-alerts)
- [Microsoft Download: Security Incident Management in Microsoft Office 365](https://download.microsoft.com/download/2/F/1/2F16A9CA-8D4F-4BB5-8F85-3A362131A95B/Office%20365%20Security%20Incident%20Management.pdf)
- [Microsoft Incident Response and shared responsibility for cloud computing](https://azure.microsoft.com/blog/microsoft-incident-response-and-shared-responsibility-for-cloud-computing/)

## Next steps

Adopt these security controls and adapt them to your organization's risk tolerance and productivity requirements. You should use a continuous improvement approach where you continuously build towards the ideal state.

Start by prioritizing controls and the minimum ideal target levels. Ensure you have positive security impact and low-friction changes first. Prioritize, implement, and integrate the first control then repeat the process with the next control.

You should prioritize the [critical foundations](#establish-critical-foundations) first because of their broad positive impact and [credential and secret scanning](#credential-and-secret-scanning) because of its high impact and frequent attacker use.
