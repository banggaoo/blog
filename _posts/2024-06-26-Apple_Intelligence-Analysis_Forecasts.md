---
title: "Apple Intelligence Analysis and Forecasts"
date: 2024-06-26
tags: [iOS, AI]
---

## [What is Apple Intelligence](https://www.apple.com/apple-intelligence/)
Apple's artificial intelligence technology and platform

## Apple Intelligence Architecture
![84d58ca4-f450-403d-b6ca-ff02cd1b2e8a](https://github.com/banggaoo/blog/assets/284765/93315695-651b-48c5-b9f0-182e83d9a6e8)

Architecture where foundation model is placed in OnDevice and Cloud respectively and orchestration is performed in OnDevice.

## Apple Intelligence Features
### Efficiency
Minimize model development costs by using the same hardware for both OnDevice and Cloud.

In the case of LLM and Stable Diffusion Model used in OnDevice, it is compressed to about 1GB.

Minimize unnecessary data input when creating models using synthetic data.

Use three methods for extreme compression.
<img width="604" alt="Screenshot 2024-06-14 at 3 50 29 PM" src="https://github.com/banggaoo/blog/assets/284765/565c9420-d352-4923-ba0d-30f10fd5f951">

### Task-specific
![9c7c7339-34a1-4cb8-9ef7-f9e0d6141a6c](https://github.com/banggaoo/blog/assets/284765/b7739f4b-187f-4c0e-94ae-903894e230b3)
A method of operating by replacing a task-specific model on top of the foundation model

### Privacy
No user information stored in the cloud.

Open sources that allow for external monitoring.

### Deep integration
iOS systems and even third-party apps can be integrated with the Apple Intelligence platform.

We provide a behavior and data sharing platform based on App Intents.

## Analysis
Apple currently has the most advanced Hybrid AI architecture.

Because LLM-based services that require high costs in the existing cloud are less sustainable, many companies are expected to give up LLM-related services or try to switch to efficient OnDevice AI like Apple.

Apple Intelligence is expected to evolve into an AI platform that can reach the deepest level of user information.

Apple's lack of ultra-large model-based AI is expected to be made up for through collaboration with OpenAI and others.

[Introducing Apple’s On-Device and Server Foundation Models](https://machinelearning.apple.com/research/introducing-apple-foundation-models)

[Platforms State of the Union](https://developer.apple.com/videos/play/wwdc2024/102/)

[Explore machine learning on Apple platforms](https://developer.apple.com/wwdc24/10223)
