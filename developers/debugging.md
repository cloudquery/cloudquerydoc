---
description: How to debug CQ providers for easier development
---

# Debugging

## Running the provider in debug mode

Debugging CQ providers is a fairly straight forward process: 

First we must run provider in debug mode, to do this set the environment variable `CQ_PROVIDER_DEBUG=1`, in our IDE or terminal and execute the provider.

The following message will appear when executing the plugin binary.

{% tabs %}
{% tab title="Windows" %}
```bash
Provider started, to attach Cloudquery set the CQ_REATTACH_PROVIDERS env var:

	Command Prompt:	set CQ_REATTACH_PROVIDERS=./providers/cq-my-provider/.cq_reattach
	PowerShell:	$env:CQ_REATTACH_PROVIDERS=./providers/cq-my-provider/.cq_reattach
```
{% endtab %}

{% tab title="Linux/OSX" %}
```bash
Provider started, to attach Cloudquery set the CQ_REATTACH_PROVIDERS env var:
        export CQ_REATTACH_PROVIDERS=/cq-my-provider/.cq_reattach
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
 Currently it is possible to debug a single provider at a given time.
{% endhint %}

Once we set up `CQ_REATTACH_PROVIDERS`, we will be able to execute any command from our CQ binary and it will use the debugged plugin instead of the latest version.

{% hint style="success" %}
We can now execute our provider from our favourite IDE in debug mode and put breakpoints to test and debug our provider
{% endhint %}

### Example

In the following example we will download an existing provider, compile it and execute it in debug mode.

```go
git clone https://github.com/cloudquery/cq-provider-aws.git
go build -o cq-provider-aws
export CQ_PROVIDER_DEBUG=1 
./cq-provider-aws // Execute the provider binary
// Provider started, to attach Cloudquery set the CQ_REATTACH_PROVIDERS env var:
//        export CQ_REATTACH_PROVIDERS=/<path_to_your_provider>/.cq_reattach
```

After executing the provider we will get a message of how to reattach our provider when we execute the main CQ binary. 

```go
// Path where we executed our aws provider
export CQ_REATTACH_PROVIDERS=/providers/cq-provider-aws/.cq_reattach
./cloudquery fetch --dsn "host=localhost user=postgres password=pass DB.name=postgres port=5432"
```

{% hint style="info" %}
The same example can be run from the IDE to add breakpoints 
{% endhint %}

