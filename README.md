# Transit Secrets Engine

## Overview

This module enables and configures the transit secrets engine in Vault.

## Example use case

Modern applications often have to handle sensitive data.  This could be anything from credit card number to National Insurance numbers. As application developers, there is a duty of care to protect this data when at rest and whilst in transit.

One way to protect this data, is to encrypt it before it is sent to its storage location. Cryptography can be very complicated to implement in applications.  Mistakes in the implementation can be very costly for a business.

Application developers can now leverage Vault to delegate encryption away from their apps and instead, rely on Vault to perform the cryptography function.  Vault will manage the keys securely and rich access controls can be implemented by leveraging Vault policies.

## Usage

```hcl
provider "vault" {
  address = "http://localhost:8200"
  token   = var.vault_token
}

variable "vault_token" {}

module "transit_defaults" {
  source          = "../../"

  transit_keys = [
    {
      name                   = "dev"
      allow_plaintext_backup = false
      convergent_encryption  = false
      exportable             = false
      deletion_allowed       = true
      derived                = false
      type                   = "rsa-2048"
      min_decryption_version = 1
      min_encryption_version = 1
    },
    {
      name                   = "staging"
      allow_plaintext_backup = false
      convergent_encryption  = false
      exportable             = false
      deletion_allowed       = true
      derived                = false
      type                   = "rsa-2048"
      min_decryption_version = 1
      min_encryption_version = 1
    }
  ]
}
```

## License

Licensed under the Apache License, Version 2.0 (the "License").

You may obtain a copy of the License at [apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0).

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an _"AS IS"_ basis, without WARRANTIES or conditions of any kind, either express or implied.

See the License for the specific language governing permissions and limitations under the License.