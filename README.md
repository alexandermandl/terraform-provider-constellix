# Constellix DNS Provider

Requirements
------------

- [Terraform](https://www.terraform.io/downloads.html) Latest Version

- [Go](https://golang.org/doc/install) go1.13.8

## Building The Provider ##
Clone this repository to: `$GOPATH/src/github.com/Constellix/terraform-provider-constellix`.

```sh
$ mkdir -p $GOPATH/src/github.com/Constellix; cd $GOPATH/src/github.com/Constellix
$ git clone https://github.com/Constellix/terraform-provider-constellix.git
```

Enter the provider directory and run make build to build the provider binary.

```sh
$ cd $GOPATH/src/github.com/Constellix/terraform-provider-constellix
$ make build

```

Using The Provider
------------------
If you are building the provider, follow the instructions to :
Installing Plugins
Third-party plugins (both providers and provisioners) can be manually installed into the user plugins directory, located at %APPDATA%\terraform. d\plugins on Windows and ~/. terraform. d/plugins on other systems.
After placing it into your plugins directory, run `terraform init` to initialize it.
ex.
```hcl
#configure provider with your Constellix  credentials.
provider "constellix" {
  # constellix Api key
  apikey = "apikey"
  # cosntellix secret key
  secretkey = "secretkey"
  insecure = true
  proxy_url = "https://proxy_server:proxy_port"
}

resource "constellix_domain" "domain1" {
  name = "domain1.com"
  soa = {
    primary_nameserver = "ns41.constellix.com."
    ttl                = 1800
    refresh            = 48100
    retry              = 7200
    expire             = 1209
    negcache           = 8000
  }
}


```
Note : If you are facing the issue of `409 conflict error` try running your Terraform configuration with parallelism set to one as mentioned below.

```
terraform plan -parallelism=1
terraform apply -parallelism=1
```  

Developing The Provider
-----------------------
If you want to work on the provider, you'll first need [Go](http://www.golang.org) installed on your machine. You'll also need to correctly setup a [GOPATH](http://golang.org/doc/code.html#GOPATH), as well as adding `$GOPATH/bin` to your `$PATH`.

To compile the provider, run `make build`. This will build the provider with sanity checks present in scripts directory and put the provider binary in `$GOPATH/bin` directory.

