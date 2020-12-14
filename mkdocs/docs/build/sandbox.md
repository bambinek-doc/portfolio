# Sandbox Environment

## Overview

With Belvo's sandbox environment, you can interact with dummy data to prototype your banking, fiscal, or gig apps and connect them to widgets or webhooks. In this article we'll provide you reference documentation on what resources are available and in which use cases you can apply them. To see them used in practice, check out our simple [banking](), [fiscal](), and [gig]() app guides. 

## Accessing the sandbox
To access the sandbox, just make sure to [generate your sandbox API keys](). 

??? example "Test your credentials"
    To make sure that everything is working as expected, try out the following API call in the sandbox environment. If you've used the right keys, you'll see a list of institutions in the response. 

    === "cURL"
        ```html
        curl https://sandbox.belvo.co/api/institutions/  \
        -u [<Secret Key ID>]:[<Secret Key PASSWORD>]

        ```

    === "Node"

        ```javascript

        // Check out our node.js SDK on github:
        // https://github.com/belvo-finance/belvo-js

        var belvo = require('belvo').default;

        var client = new belvo(
        'Secret Key ID',
        'Secret Key PASSWORD',
        'https://sandbox.belvo.co'
        );

        client.connect()
        .then(function () {
            client.institutions.list()
            .then(function (res) {
                console.log(res);
            })
            .catch(function (error) {
                console.log(error);
            });
        });

        ```
    
    === "Python"

        ```python
        # Check out our python SDK on github:
        # https://github.com/belvo-finance/belvo-python
        from pprint import pprint
        from belvo.client import Client

        # Login to Belvo API
        client = Client("Secret Key ID", "Secret Key PASSWORD", "https://sandbox.belvo.co")

        # List institutions
        for institution in client.Institutions.list():
            pprint(institution)

        ```

    === "Ruby"

        ```ruby
        # Check out our Ruby SDK on github:
        # https://github.com/belvo-finance/belvo-ruby
        require 'belvo'

        sandbox = Belvo::Client.new(
        'Secret Key ID',
        'Secret Key PASSWORD',
        'https://sandbox.belvo.co'
        )

        sandbox.institutions.list

        ```
    Working as expected?

    [Yep! 👍](#){: .md-button } [I'm having issues 😔](#){: .md-button }


## Demo Datasets

To help you simulate real-world interactions you can use our mock data sets for banking, fiscal, and gig-economy use cases.

### Banking

For banking use cases, you have access to the following retail institutions:

=== "Erebor Bank"

    - `erebor_mx_retail`
    - `erebor_co_retail`
    - `erebor_br_retail`


=== "Gringotts Bank"

    - `gringotts_mx_retail`
    - `gringotts_co_retail`
    - `gringotts_br_retail`

You can simulate different types of users by using the following account credentials:

| Use case| Username | Password | Description|
| -------------------------------- | -------- | -------- | -------------------------------------------------------------- |
| Full Data | `bnk100`   | `full`     |  Paginated data, including transactions, owners, accounts, loans, credits, income, and statements. |
| No Data| `bnk101`   | `nodata`   | Link with no data. |
| Low Data| `bnk102`   | `low`      | Non-paginated data set.|
| Negative Balance| `bnk103`   | `negative` | Non-paginated data set with negative values. |

??? tip "Try it out"

### Fiscal

For fiscal use cases, you have access to the following institution:

=== "Tatooine Fiscal"

    - `tatooine_mx_fiscal` 




| Use Case| Username  | Password | Description|
| ------------------------------- | --------- | -------- | ------------------------------------------------------------------- |
| Full Data | `fiscal100` | `full`| Full dataset of fiscal information, that includes paginated invoices (outflow and inflow), tax status, and tax returns. |
| No Data| `fiscal101` | `nodata`| Link with no data.|
| Low Data| `fiscal102` | `low`| Non-paginated data set.|

??? tip "Try it out"

### Gig Economy

For gig-economy use cases, you have access to the following institutions:

=== "Goonies"

    Goonies is a mock ride-sharing company.

    - `goonies_mx_retail`
    - `goonies_co_retail`
    - `goonies_br_retail`

=== "Planet Express"

    Planet Express is a mock delivery company.

    - `planet_mx_retail`
    - `planet_co_retail`
    - `planet_br_retail`



| Use case| Username | Password | Description|
| ---------------------------- | -------- | -------- | -------------------------------------------------------------------------- |
| Full Data | `gig100`   | `full`| Complete paginated dataset that will cover our entire data schema (transactions, owners, accounts, loans, credits, income, statements). |
| No Data| `gig101`   | `nodata`| A link that won't generate any kind of data.|
| Low Data| `gig102`   | `low`| Non-paginated data set.|
| Negative Balance| `gig103`   | `negative` | Same case than _low data_ but with a negative balance.|

??? tip "Try it out"

## Standard Flows

When you want to test standard user login flows for an API or widget, you can use these credentials for any institution:

| Case                | Username          | Password          |  Response            |
| ------------------- | ----------------- | ----------------- |  ------------------- |
| Valid credentials   | `user_valid`       | `pass_valid`       |  200 Success         |
| Invalid credentials | `user_invalid`     | `pass_invalid`     |  400 Login Error      |
| Validation error    | `1234567890abcdefg` | `1234567890abcdefg` |  400 Validation Error |

??? tip "Try it out"

!!! error "400 Duplication Error"
    If you create more than one [`link`]() for an institution using the same credentials, you'll receive a **400 Duplication Error**.
    To avoid this error, make sure you use unique `username` and `password` combinations.


## Advanced Link Flows

When you want to test out advanced user login flows that require additional `username_type`, `username2`, or `password2` parameters, you can use the following institution and credentials:

=== "Iron Bank"

    - `ironbank_br_business`
    - `ironbank_br_retail` 


| Case                | Username     | Password      | Username type | Username2 | Password2 | API Response    |
| ------------------- | ------------ | ------------- | ------------- | --------- | --------- | --------------- |
| Valid credentials   | `adv_valid`   | `pass_valid`   | `003`           | `valid`     | `valid`     | 200 Success     |
| Invalid credentials | `adv_invalid` | `pass_invalid` | `999`           | `invalid`   | `invalid`   | 400 Login Error |

??? tip "Try it out"

## Two-Factor Authentication

When you want to test out user login flows that require two-factor authentication (2FA), you can use the following institutions:

=== "Gotham Business Bank"

    - `gotham_mx_retail`
    - `gotham_co_retail`
    - `gotham_br_retail`

=== "Heimdall Bank "

    - `heimdall_mx_retail`
    - `heimdall_co_retail`
    - `heimdall_br_retail`


Depending on the flow you want to simulate, use the appropriate username and password:

| Simulate a flow where a user needs to: | Username| Password|
| ----------------------- | ------------ | ------------- |
| generate 2FA using a mobile or other device. | `mfa_default` | `pass_valid`   | 
| scan a QR code in order to generate the 2FA token.           | `mfa_qr`      | `qr_code` |
| input a challenge code in order to generate the 2FA token.                 | `mfa_numeric` | `numeric_code` |

After you use one of these credentials, you'll receive a 428 HTTP response. You'll need to **PATCH** the link with one of the following tokens to finish creating the link.

| Case          | Value  | API Response       |
| ------------- | ------ | ------------------ |
| Valid token   | `111111` | 201 Created        |
| Invalid token | `999999` | 428 Token Required |

??? tip "Try it out"

!!! info
    In the case where you use an invalid token, we simulate the scenario where the user enters a wrong token. As a result, you'll receive a new 428 response, asking again for a new token.


**How useful was this article?**

[⭐️](#){: .md-button .md-button--primary} [⭐️⭐️](#){: .md-button .md-button--primary} [⭐️⭐️⭐️](#){: .md-button .md-button--primary}

