# EvolvKit
[![Version](https://img.shields.io/cocoapods/v/EvolvKit.svg?style=flat)](https://cocoapods.org/pods/EvolvKit)
[![License](https://img.shields.io/cocoapods/l/EvolvKit.svg?style=flat)](https://cocoapods.org/pods/EvolvKit)
[![Platform](https://img.shields.io/cocoapods/p/EvolvKit.svg?style=flat)](https://cocoapods.org/pods/EvolvKit)

## Example

To run the example project, clone the repo, and run `pod install` from the Example directory first.

## Requirements
cocoapods
```ruby
sudo gem install cocoapods
```

## Installation

EvolvKit is available through [CocoaPods](https://cocoapods.org/pods/EvolvKit). To install
it, simply add the following line to your Podfile:

```ruby
pod 'EvolvKit'
```

## License

EvolvKit is available under the Apache License, Version 2.0. See the LICENSE file for more info.

## How to use the EvolvKit SDK

#### Vocabulary

**Participant:** The end user of the application, the individual who's actions are being recorded in the experiment.
**Allocation:** The set of configurations that have been given to the participant, the values that are being
experimented against.
**Candidate** The specific group of variants in the allocation.
**Variant** The different values each variable can have.

For a complete example of how to use this SDK see our [example app](https://github.com/evolv-ai/EvolvKit/tree/master/Example).

### Import the SDK

1. Import the Evolv SDK.
```swift
import EvolvKit
```

### Participant Initialization

1. Build an EvolvParticipant instance.
```swift
let participant = EvolvParticipant.builder().build()

or 

let participant = EvolvParticipant.builder().(userId: <custom_id>).build()
```
*Note: If you do not set the participant's userId, the builder will create a unique id for you.*


### Client Initialization

1. Build an EvolvConfig instance.
```swift
let config: EvolvConfig = EvolvConfig.builder(environmentId: <environment_id>, httpClient: <http_client>).build()
```

2. Initialize the EvolvClient.
```swift
let client: EvolvClient = EvolvClientFactory.createClient(config: config)
```

### Confirm the Allocation

1. The call to ‘confirm’ should send a confirmation for every candidate that a user has been allocated into with the corresponding experiment.
Evolv SDK will keep a record of every candidate that requested a variant. When ‘confirm’ is called, Evolv will send confirmation for those candidates.
```swift
client.confirm()
```
*Note: After the client has been initialized, it is important to confirm the participant into the experiment. This action
records the participant's allocation and sends the information back to Evolv.*


### Value Subscription

You may want to use a value from your allocation without blocking the execution of your application. If this is true, you can
subscribe to a value and apply any actions as a result of it asynchronously.

1. Subscribe to a value from Evolv.
```swift
client.subscribe(forKey: <key_for_value>, defaultValue: <default_value>, closure: <closure>)
```

*Note: The return value's type is decided by the provided default value's type. If there is an issue retrieving the
requested value, the default value will be returned in its place. If you have a previous allocation stored the 
value will be retrieved and then your code will be executed. When the new allocation is retrieved if the value
differs from the previously stored allocation then your code will be ran again with the new value. If your code 
results in an Exception it will be thrown.*

### Custom Events (optional)

Sometimes you may want to record certain events that occurred during the participant's session. An example of an event
thats important to record is a "conversion" event. If you implemented the SDK in a shopping app, you could send the
"conversion" event when the participant presses the checkout button.

1. Emit a custom event.
```swift
client.emitEvent(forKey: <event_type>)
```

AND / OR

2. Emit a custom event with an associated score.
```swift
client.emitEvent(forKey: <event_type>, score: <score>)
```

### Contaminate the Allocation (optional)

Sometimes it may be necessary to contaminate the participant's allocation. Meaning, that you may not want that participant's session to be recorded into the experiment.

1. Contaminate the participant's allocation.
```swift
client.contaminate()
```    

### Custom Allocation Store (optional)

Once a participant has been allocated into an experiment you may want to retain the allocations they received. To do this, create a custom allocation store by
implementing the EvolvAllocationStore interface. You can supply the custom allocation store to the client when you build the EvolvConfig.

1. Supply the allocation store to the client.
```swift
let config = EvolvConfig.builder(environmentId: <environment_id>, httpClient: <http_client>)
    .set(allocationStore: <custom_store>)
    .build()

let client = EvolvClientFactory.createClient(config: config,
                                             participant: EvolvParticipant.builder().set(userId: "sandbox_user").build())
```


### Optional Configurations

There are several optional configurations available through the EvolvConfig builder, check out the EvolvConfig
documentation to see what options are available.


### About Evolv and the Evolv Product

Evolv Delivers Autonomous Optimization Across Web & Mobile.

You can find out more by visiting: https://www.evolv.ai/



<h1 align="center">Welcome to - Client</h1>
<p>
  <img alt="Version" src="https://img.shields.io/badge/version-1.0.0-blue.svg?cacheSeconds=2592000" />
  <img src="https://img.shields.io/badge/node-%3E%3D13-blue.svg" />
  <a href="https://github.com/evolv-ai/javascript-sdk#readme" target="_blank">
    <img alt="Documentation" src="https://img.shields.io/badge/documentation-yes-brightgreen.svg" />
  </a>
  <a href="https://github.com/evolv-ai/javascript-sdk/graphs/commit-activity" target="_blank">
    <img alt="Maintenance" src="https://img.shields.io/badge/Maintained%3F-yes-green.svg" />
  </a>
</p>

> This is the official client for the optimization platform.

Documentation can be found here: https://example.com/swift-sdk/releases/latest/docs/EvolvClient.html

### [Homepage](https://www.example.com)

## Prerequisites

- node >=13

## Install

```sh
npm install
```

## Documentation Build

```sh
npm run docs
```

## Development Build

```sh
npm run build
```

## Production Build

```sh
npm run build-prod
```

## Run tests

```sh
npm test
```

## Author

**[Test Technologies](support@example.com)**


## Contributing

Contributions, issues and feature requests are welcome!<br />Feel free to check [issues page](https://github.com/dvoineu/electron-todo-app/swift-sdk/issues). You can also take a look at the [contributing guide](https://github.com/dvoineu/electron-todo-app/swift-sdk/blob/master/CONTRIBUTING.md).


## License

This project is [MIT](https://github.com/dvoineu/electron-todo-app/swift-sdk/blob/master/LICENSE) licensed.
