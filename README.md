# cdktf-go-azurerm
Example of provisioning azurerm resources in Go via terraform-cdk.

## Requirements
* [cdktf](https://github.com/hashicorp/terraform-cdk) 0.7.0
* your favourite text editor

## Setup
To set up [azurerm provider](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs) either set `ARM*` environment variables or modify the [relevant section](https://github.com/waxb/cdktf-go-azurerm/blob/cd4a46ebc590088ab39967281b578a954db1a1cd/main.go#L16), I left the Subscription ID line as an example.

NOTE: You either need to set `NODE_OPTIONS` environment variable to 16GBs via
```
export NODE_OPTIONS='--max_old_space_size=15000'
```
or invoke `cdktf` with the command below. [See](https://github.com/hashicorp/terraform-cdk/issues/1264)
```
git clone https://github.com/waxb/cdktf-go-azurerm.git && cd cdktf-go-azurerm
NODE_OPTIONS='--max_old_space_size=16384' cdktf get
```
If you don't have 16GBs of memory, you can get the generated go provider from [here](https://github.com/waxb/azurerm)
Go to the directory where this repository was cloned:
```
mkdir -p generated/hashicorp && cd $_
git clone https://github.com/waxb/azurerm.git
```

## Create test infrastructure
```
cdktf deploy
```

## Covered examples
* Provider initialisation [1](https://github.com/waxb/cdktf-go-azurerm/blob/cd4a46ebc590088ab39967281b578a954db1a1cd/main.go#L16)
* Module instance creation [1](https://github.com/waxb/cdktf-go-azurerm/blob/cd4a46ebc590088ab39967281b578a954db1a1cd/main.go#L21) [2](https://github.com/waxb/cdktf-go-azurerm/blob/cd4a46ebc590088ab39967281b578a954db1a1cd/main.go#L28) (Null Module at the moment because of limitations, [see](https://github.com/Azure/terraform-azurerm-naming/issues/64))
* Resource creation and reference [1](https://github.com/waxb/cdktf-go-azurerm/blob/cd4a46ebc590088ab39967281b578a954db1a1cd/main.go#L35) [2](https://github.com/waxb/cdktf-go-azurerm/blob/cd4a46ebc590088ab39967281b578a954db1a1cd/main.go#L42) [3](https://github.com/waxb/cdktf-go-azurerm/blob/cd4a46ebc590088ab39967281b578a954db1a1cd/main.go#L49) [4](https://github.com/waxb/cdktf-go-azurerm/blob/cd4a46ebc590088ab39967281b578a954db1a1cd/main.go#L57) [5](https://github.com/waxb/cdktf-go-azurerm/blob/cd4a46ebc590088ab39967281b578a954db1a1cd/main.go#L69)
* Terraform built in [function](https://www.terraform.io/docs/language/functions/file.html) usage [1]((https://github.com/waxb/cdktf-go-azurerm/blob/cd4a46ebc590088ab39967281b578a954db1a1cd/main.go#L79))
* Module output reference [1]((https://github.com/waxb/cdktf-go-azurerm/blob/cd4a46ebc590088ab39967281b578a954db1a1cd/main.go#L97))
* Multiple outputs [1]((https://github.com/waxb/cdktf-go-azurerm/blob/cd4a46ebc590088ab39967281b578a954db1a1cd/main.go#L97))

## Cleanup
Do not forget to clean up the mess we've caused at microsoft, they have enough money and overused compute resources already!
```
cdktf destroy
```
