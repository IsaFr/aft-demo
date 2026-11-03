# ApexLibra Callout Framework

Imported unchanged from [Apex-Opensource-Library](https://github.com/pkozuchowski/Apex-Opensource-Library/tree/25ca32b0da67bffd60d029fbe4419decc645edd5/force-app/commons/callout), commit `25ca32b0da67bffd60d029fbe4419decc645edd5`.

Upstream documentation: https://apexlibra.org/apex/callout

## Components

The framework classes are `Callout`, `CalloutConditions`, `CalloutHandlers`, `CalloutHandlersList`, and `CalloutResponseException`. Shared dependencies are `Condition`, `Conditions`, and `Runtime`. The upstream tests are `CalloutTest`, `ConditionsTest`, and `RuntimeTest`. All class files and their metadata live in `force-app/main/default/classes`.

MIT license: [apexlibra-MIT.txt](../licenses/apexlibra-MIT.txt). Original license headers are preserved in the source.

## Example

Configure a Named Credential for your actual endpoint before running an integration:

```apex
Callout request = new Callout();
request.setMethod('GET');
request.setEndpoint('callout:YourNamedCredential/accounts');
request.setResponseType(List<Account>.class);
List<Account> accounts = (List<Account>) request.execute();
```

The default handlers retry unauthorized and timeout responses once, throw exceptions for errors, and deserialize successful JSON responses. The logging handler is an upstream placeholder; connect it to your own logger if needed.

## Validate without deploying

```sh
sf project deploy start --source-dir force-app/main/default/classes --target-org dev --dry-run --test-level RunSpecifiedTests --tests CalloutTest ConditionsTest RuntimeTest --wait 10
```

To deploy and run the same tests, omit `--dry-run` and explicitly choose the intended target org.
