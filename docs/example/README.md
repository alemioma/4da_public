# README: Example Service Providers for TDPnet

## Overview

This folder contains a collection of example Service Providers (SPs) for TDPnet, grouped by different programming platforms. Each example is crafted to demonstrate the implementation of SPs in various programming environments, providing a practical reference for developers.

## Platform-Specific Examples

The examples are categorized based on the programming platform used. This allows developers familiar with a particular platform to easily find relevant examples. Currently, the following platforms are covered:

- **Node.js:** JavaScript runtime built on Chrome's V8 JavaScript engine, ideal for building fast, scalable network applications.
- **C++:** A high-performance programming language used extensively in system/software development.
- **.NET:** A free, cross-platform, open-source developer platform for building many different types of applications.
- **Python:** A high-level, interpreted, and general-purpose programming language known for its readability and versatility.

## Example Pattern

All examples follow a consistent design pattern, making it easier to understand and adapt the code across different platforms. This pattern includes:

1. **Class Session:** Manages communication with the network. Key methods include `onCommand(data)` for receiving messages and `send(id, data)` for sending messages. It utilizes `socket.io` for managing network interactions.

2. **Class Prompt:** Inherits from Session. Implements `onCommand(data)` by inspecting `data.subject`. Declares virtual `onXXX` methods for each `XXX` subject and defines methods named `YYY` corresponding to the subjects of outgoing messages.

3. **Class App:** Inherits from Prompt. Implements `onXXX` methods to respond using the `YYY` methods.

Every App must establish a network connection using the `connect` method from Session. Upon connection (`onConnected`), the App should execute the `signin` method (Session). Two main events can occur:
   - `onDenied`: Indicates the App is using incorrect credentials.
   - `onGranted`: Grants the App access to the network, allowing interaction with other SPs.

## Navigating the Examples

Each platform-specific directory contains a set of examples. These examples are designed to provide clear insights into the development of SPs for TDPnet within that specific programming environment. They cover a range of topics from basic setup to more advanced functionalities.

### What You'll Find in Each Example:

- **Source Code:** Fully functional example codes.
- **Documentation:** Comments and README files explaining the code's functionality and how it integrates with TDPnet.
- **Configuration Files:** Necessary configuration files to set up and run the examples.

## Getting Started

To get started with these examples:

1. **Choose Your Platform:** Navigate to the folder of the platform you are comfortable with or wish to explore.
2. **Explore the Examples:** Read the documentation provided with each example to understand its purpose and implementation.
3. **Run and Experiment:** Execute the examples to see them in action. Feel free to modify and experiment with the code to gain a deeper understanding.

## Contribution

These examples are intended to be living documents, evolving with contributions from the TDPnet community. If you have an example you'd like to add or an improvement to an existing one, please feel free to contribute.

---

*These examples are designed to help developers learn how to write effective Service Providers for TDPnet across various platforms. They are meant for educational purposes and should be adapted as needed for production environments.*
