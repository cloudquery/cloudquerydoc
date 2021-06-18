---
description: How to write policies
---

# Policy

Policies are very useful to define security, governance, cost and compliance rules but in theory they can be used
for many other purposes as well since they're basically a set of SQL queries.

A policy usually consist of at least one database query that can be seen as a rule (or constraint) and that dictates 
cloudquery how and what should be executed by the internal policy execution system. However, cloudquery's policy engine 
is quite powerful and allows the user to create a complex policy hierarchy for sophisticated policy development.

Views can be used to define certain queries that may help other queries to reduce their complexity and to be able to 
define reusable queries.

## Simple Example

The example below shows a simple policy definition:

```text
policy "test-policy" {
  description = "This is a test policy"
  configuration {
    provider "aws" {
      version = ">= 1.0"
    }
  }

  query "top-level-query" {
    description = "Top Level Query"
    query = "SELECT * FROM test_policy_table WHERE name LIKE 'peter'"
  }
}
```

Every policy starts with the `policy` tag and a label (e.g. `test-policy`). A `description` helps other users to figure
out the purpose of this policy. 
The `configuration` block defines configuration settings for your policy e.g. which provider is required for this policy
and the minimal version.
Ultimately, the policy should contain a query that gets executed on policy run.

## Policy Views

Policy views can be used to simplify query SQL commands by defining sub queries that can be reused within other queries
or even other views. CloudQuery only creates temporary views and creates them before query execution.

{% hint style="info" %}
Since CloudQuery uses the view tags name for the actual database view name it is not allowed to use specific characters 
like dashes ("-").
{% endhint %}

```text
policy "test-policy" {
  description = "This is a test policy"
  configuration {
    provider "aws" {
      version = ">= 1.0"
    }
  }
  
  view "myview" {
    description = "My awesome view"
    query "complex-query" {
        query = "SELECT * FROM test_policy_table WHERE name LIKE 'john'"
    } 
  }

  query "top-level-query" {
    description = "Top Level Query"
    query = "SELECT * FROM myview"
  }
}
```

As you can see, the query command got significantly simplified and makes it much easier to read.
It is a good practice to use views if multiple queries use certain sub queries multiple times.

## Policy inside policy (inception)

It is possible to define policies inside policies inside polices (and so on...) to build a policy hierarchy.

```text
policy "test-policy" {
  description = "Test Policy"
  configuration {
    provider "aws" {
      version = ">= 1.0"
    }
  }

  view "testview" {
    description = "Test View"
    query "testviewquery" {
      query = "SELECT * FROM test_policy_table WHERE name LIKE 'john'"
    }
  }

  query "top-level-query" {
    description = "Top Level Query"
    query = "SELECT * FROM test_policy_table WHERE name LIKE 'peter'"
  }

  policy "sub-policy-1" {
    description = "Sub Policy 1"
    query "sub-level-query" {
      query = "SELECT * from testview"
      expect_output = true
    }
    
    policy "sub-sub-policy-1" {
    description = "Sub Sub Policy 1"
    query "sub-sub-level-query" {
      query = "SELECT * from test_policy_table WHERE name LIKE 'peter'"
    }
  }
  }
  
  policy "sub-policy-2" {
    description = "Sub Policy 2"
    query "sub-level-query" {
      query = "SELECT * from test_policy_table WHERE name LIKE 'peter'"
    }
  }
}
```


