# OpenFaas Templates customized

Contains customized templates for internal use.

# OpenFaaS Classic templates

[![Build Status](https://github.com/openfaas/templates/workflows/ci-only/badge.svg?branch=master)](https://github.com/openfaas/templates/actions)

To find out more about the OpenFaaS templates see the [faas-cli](https://github.com/openfaas/faas-cli).

> Note: The templates are completely customizable - so if you want to alter them please do fork them and use `faas template pull` to make use of your updated versions.

### WHJR Specific Templates

This repository contains the OpenFaaS templates. Read above for more information.

| Name | Language | Version | Linux base | Watchdog | Link
|:-----|:---------|:--------|:-----------|:---------|:----
| node12-whjr | NodeJS | 12 | Alpine Linux | of-watchdog | [NodeJS template](https://github.com/openfaas/templates/tree/master/template/node12)
| python3-whjr | Python | 3 | Alpine Linux | classic | [Python 3 template](https://github.com/openfaas/templates/tree/master/template/python3)

For more information on the templates check out the [docs](https://docs.openfaas.com/cli/templates/).

### Classic vs of-watchdog templates

The current version of OpenFaaS templates use the original `watchdog` which `forks` processes - a bit like CGI. The newer watchdog [of-watchdog](https://github.com/openfaas-incubator/of-watchdog) is more similar to fastCGI/HTTP and should be used for any benchmarking or performance testing along with one of the newer templates. Contact the project for more information.


### License

This project is part of the OpenFaaS project licensed under the MIT License.
