# az-linuxappservice-tf

<!-- BEGIN_TF_DOCS -->
## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | ~> 1.4.0 |
| <a name="requirement_azurerm"></a> [azurerm](#requirement\_azurerm) | ~> 3.20 |

## Providers

| Name | Version |
|------|---------|
| <a name="provider_azurerm"></a> [azurerm](#provider\_azurerm) | ~> 3.20 |
| <a name="provider_azurerm.logs"></a> [azurerm.logs](#provider\_azurerm.logs) | ~> 3.20 |

## Modules

No modules.

## Resources

| Name | Type |
|------|------|
| [azurerm_linux_web_app.web_app](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/linux_web_app) | resource |
| [azurerm_monitor_diagnostic_setting.acr_diagnostics](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/monitor_diagnostic_setting) | resource |
| [azurerm_log_analytics_workspace.logs](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/data-sources/log_analytics_workspace) | data source |
| [azurerm_service_plan.service_plan](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/data-sources/service_plan) | data source |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_always_on"></a> [always\_on](#input\_always\_on) | Force HTTPS connections | `bool` | `true` | no |
| <a name="input_api_definition_url"></a> [api\_definition\_url](#input\_api\_definition\_url) | URL to API definition | `string` | `null` | no |
| <a name="input_api_management_api_id"></a> [api\_management\_api\_id](#input\_api\_management\_api\_id) | Associated API Management ID | `string` | `null` | no |
| <a name="input_app_command_line"></a> [app\_command\_line](#input\_app\_command\_line) | App command line to launch app | `string` | `null` | no |
| <a name="input_app_settings"></a> [app\_settings](#input\_app\_settings) | Key-Value pairs of app settings | `map(string)` | `{}` | no |
| <a name="input_application_stack"></a> [application\_stack](#input\_application\_stack) | Application stack settings | <pre>object({<br>    docker_image        = optional(string)<br>    docker_image_tag    = optional(string)<br>    dotnet_version      = optional(string)<br>    go_version          = optional(string)<br>    java_server         = optional(string)<br>    java_server_version = optional(string)<br>    java_version        = optional(string)<br>    node_version        = optional(string)<br>    php_version         = optional(string)<br>    python_version      = optional(string)<br>    ruby_version        = optional(string)<br>  })</pre> | n/a | yes |
| <a name="input_auth_settings_v2"></a> [auth\_settings\_v2](#input\_auth\_settings\_v2) | Authentication settings | <pre>object({<br>    auth_enabled                            = optional(bool, true)<br>    runtime_version                         = optional(string, "~1")<br>    config_file_path                        = optional(string)<br>    require_authentication                  = optional(bool, true)<br>    unauthenticated_action                  = optional(string, "RedirectToLoginPage")<br>    default_provider                        = optional(string)<br>    excluded_paths                          = optional(list(string))<br>    http_route_api_prefix                   = optional(string, "/.auth")<br>    forward_proxy_convention                = optional(string, "ForwardProxyConventionNoProxy")<br>    forward_proxy_custom_host_header_name   = optional(string)<br>    forward_proxy_custom_scheme_header_name = optional(string)<br>    apple_v2 = optional(object({<br>      client_id                  = string<br>      client_secret_setting_name = string<br>    }))<br>    active_directory_v2 = optional(object({<br>      tenant_auth_endpoint                 = string<br>      client_id                            = string<br>      client_secret_setting_name           = optional(string)<br>      client_secret_certificate_thumbprint = optional(string)<br>      jwt_allowed_groups                   = optional(list(string))<br>      jwt_allowed_client_applications      = optional(list(string))<br>      www_authentication_disabled          = optional(bool, false)<br>      allowed_groups                       = optional(list(string))<br>      allowed_identities                   = optional(list(string))<br>      allowed_applications                 = optional(list(string))<br>      login_parameters                     = optional(map(string))<br>      allowed_audiences                    = optional(list(string))<br>    }))<br>    azure_static_web_app_v2 = optional(object({<br>      client_id = string<br>    }))<br>    custom_oidc_v2 = optional(list(object({<br>      name                          = string<br>      client_id                     = string<br>      openid_configuration_endpoint = string<br>      name_claim_type               = optional(string)<br>      scopes                        = optional(list(string))<br>      client_credential_method      = string<br>      client_secret_setting_name    = string<br>      authorisation_endpoint        = string<br>      token_endpoint                = string<br>      issuer_endpoint               = string<br>      certification_uri             = string<br>    })))<br>    facebook_v2 = optional(object({<br>      app_id                  = string<br>      app_secret_setting_name = string<br>      graph_api_version       = optional(string)<br>      login_scopes            = optional(list(string))<br>    }))<br>    github_v2 = optional(object({<br>      client_id                  = string<br>      client_secret_setting_name = string<br>      login_scopes               = optional(list(string))<br>    }))<br>    google_v2 = optional(object({<br>      client_id                  = string<br>      client_secret_setting_name = string<br>      allowed_audiences          = optional(list(string))<br>      login_scopes               = optional(list(string))<br>    }))<br>    microsoft_v2 = optional(object({<br>      client_id                  = string<br>      client_secret_setting_name = string<br>      allowed_audiences          = optional(list(string))<br>      login_scopes               = optional(list(string))<br>    }))<br>    twitter_v2 = optional(object({<br>      consumer_key                 = string<br>      consumer_secret_setting_name = string<br>    }))<br>    login = object({<br>      logout_endpoint                   = optional(string)<br>      token_store_enabled               = optional(bool, false)<br>      token_refresh_extension_time      = optional(number, 72)<br>      token_store_path                  = optional(string)<br>      token_store_sas_setting_name      = optional(string)<br>      preserve_url_fragments_for_logins = optional(bool, false)<br>      allowed_external_redirect_urls    = optional(list(string))<br>      cookie_expiration_convention      = optional(string, "FixedTime")<br>      cookie_expiration_time            = optional(string, "08:00:00")<br>      validate_nonce                    = optional(bool, true)<br>      nonce_expiration_time             = optional(string, "05:00:00")<br>    })<br>  })</pre> | `null` | no |
| <a name="input_auto_heal_enabled"></a> [auto\_heal\_enabled](#input\_auto\_heal\_enabled) | Enable auto-heal | `bool` | `true` | no |
| <a name="input_auto_heal_setting"></a> [auto\_heal\_setting](#input\_auto\_heal\_setting) | Auto heal settings | <pre>object({<br>    minimum_process_execution_time = string<br>    requests = optional(list(object({<br>      count    = number<br>      interval = string<br>    })))<br>    slow_requests = optional(list(object({<br>      count      = number<br>      interval   = string<br>      time_taken = string<br>      path       = optional(string)<br>    })))<br>    status_codes = optional(list(object({<br>      count             = number<br>      interval          = string<br>      status_code_range = string<br>      path              = optional(string)<br>      sub_status        = optional(number)<br>      win32_status      = optional(number)<br>    })))<br>  })</pre> | n/a | yes |
| <a name="input_backup"></a> [backup](#input\_backup) | Backup settings | <pre>object({<br>    name                     = string<br>    storage_account_url      = string<br>    enabled                  = optional(bool, true)<br>    frequency_interval       = number<br>    frequency_unit           = string<br>    keep_at_least_one_backup = optional(bool, false)<br>    retention_period_days    = number<br>  })</pre> | `null` | no |
| <a name="input_client_affinity_enabled"></a> [client\_affinity\_enabled](#input\_client\_affinity\_enabled) | Enable cookie affinity | `bool` | `false` | no |
| <a name="input_client_certificate_enabled"></a> [client\_certificate\_enabled](#input\_client\_certificate\_enabled) | Enable client certificate | `bool` | `false` | no |
| <a name="input_client_certificate_exclusion_paths"></a> [client\_certificate\_exclusion\_paths](#input\_client\_certificate\_exclusion\_paths) | Exclude URL paths from client certificate check | `string` | `null` | no |
| <a name="input_client_certificate_mode"></a> [client\_certificate\_mode](#input\_client\_certificate\_mode) | Access settings for client certificate | `string` | `"Required"` | no |
| <a name="input_connection_strings"></a> [connection\_strings](#input\_connection\_strings) | Connection strings for the app | <pre>list(object({<br>    name  = string<br>    type  = string<br>    value = string<br>  }))</pre> | `[]` | no |
| <a name="input_container_registry_managed_identity_client_id"></a> [container\_registry\_managed\_identity\_client\_id](#input\_container\_registry\_managed\_identity\_client\_id) | The Client ID of the Managed Service Identity to use for connections to the Azure Container Registry. | `string` | `null` | no |
| <a name="input_container_registry_use_managed_identity"></a> [container\_registry\_use\_managed\_identity](#input\_container\_registry\_use\_managed\_identity) | Should connections for Azure Container Registry use Managed Identity. | `bool` | `false` | no |
| <a name="input_cors"></a> [cors](#input\_cors) | Cross Origin Resource Sharing settings | <pre>object({<br>    allowed_origins     = list(string)<br>    support_credentials = optional(bool, false)<br>  })</pre> | `null` | no |
| <a name="input_default_documents"></a> [default\_documents](#input\_default\_documents) | Specifies a list of Default Documents for the Linux Web App. | `list(string)` | `null` | no |
| <a name="input_enabled"></a> [enabled](#input\_enabled) | Enable web app | `bool` | `true` | no |
| <a name="input_health_check_eviction_time_in_min"></a> [health\_check\_eviction\_time\_in\_min](#input\_health\_check\_eviction\_time\_in\_min) | The amount of time in minutes that a node can be unhealthy before being removed from the load balancer. Possible values are between 2 and 10. Only valid in conjunction with health\_check\_path. | `number` | `2` | no |
| <a name="input_health_check_path"></a> [health\_check\_path](#input\_health\_check\_path) | The path to the Health Check. | `string` | n/a | yes |
| <a name="input_https_only"></a> [https\_only](#input\_https\_only) | Force HTTPS connections | `bool` | `true` | no |
| <a name="input_ip_restrictions"></a> [ip\_restrictions](#input\_ip\_restrictions) | IP restrictions for the app | <pre>list(object({<br>    name                      = string<br>    action                    = optional(string, "Allow")<br>    ip_address                = optional(string)<br>    priority                  = number<br>    service_tag               = optional(string)<br>    virtual_network_subnet_id = optional(string)<br>    headers = optional(object({<br>      x_azure_fdid      = optional(string)<br>      x_fd_health_probe = optional(string)<br>      x_forwarded_for   = optional(string)<br>      x_forwarded_host  = optional(string)<br>    }))<br>  }))</pre> | `[]` | no |
| <a name="input_load_balancing_mode"></a> [load\_balancing\_mode](#input\_load\_balancing\_mode) | The Site load balancing. Possible values include: WeightedRoundRobin, LeastRequests, LeastResponseTime, WeightedTotalTraffic, RequestHash, PerSiteRoundRobin. | `string` | `"LeastRequests"` | no |
| <a name="input_local_mysql_enabled"></a> [local\_mysql\_enabled](#input\_local\_mysql\_enabled) | Use Local MySQL | `bool` | `false` | no |
| <a name="input_log_analytics_workspace_name"></a> [log\_analytics\_workspace\_name](#input\_log\_analytics\_workspace\_name) | Name of Log Analytics Workspace to send diagnostics | `string` | n/a | yes |
| <a name="input_log_analytics_workspace_resource_group_name"></a> [log\_analytics\_workspace\_resource\_group\_name](#input\_log\_analytics\_workspace\_resource\_group\_name) | Resource Group of Log Analytics Workspace to send diagnostics | `string` | n/a | yes |
| <a name="input_logs"></a> [logs](#input\_logs) | Logging settings | <pre>object({<br>    detailed_error_messages = optional(bool, true)<br>    failed_request_tracing  = optional(bool, true)<br>    application_logs = object({<br>      file_system_level = optional(string, "Information")<br>      azure_blob_storage = object({<br>        level             = optional(string, "Information")<br>        retention_in_days = optional(number, 365)<br>        sas_url           = string<br>      })<br>    })<br>    http_logs = object({<br>      azure_blob_storage_http = object({<br>        retention_in_days = optional(number, 365)<br>        sas_url           = string<br>      })<br>      file_system = object({<br>        retention_in_days = optional(number, 365)<br>        retention_in_mb   = number<br>      })<br>    })<br>  })</pre> | n/a | yes |
| <a name="input_resource_group_name"></a> [resource\_group\_name](#input\_resource\_group\_name) | The name of the resource group to deploy the web app to | `string` | n/a | yes |
| <a name="input_scm_ip_restrictions"></a> [scm\_ip\_restrictions](#input\_scm\_ip\_restrictions) | IP restrictions for the app | <pre>list(object({<br>    name                      = string<br>    action                    = optional(string, "Allow")<br>    ip_address                = optional(string)<br>    priority                  = number<br>    service_tag               = optional(string)<br>    virtual_network_subnet_id = optional(string)<br>    headers = optional(object({<br>      x_azure_fdid      = optional(string)<br>      x_fd_health_probe = optional(string)<br>      x_forwarded_for   = optional(string)<br>      x_forwarded_host  = optional(string)<br>    }))<br>  }))</pre> | `[]` | no |
| <a name="input_scm_use_main_ip_restriction"></a> [scm\_use\_main\_ip\_restriction](#input\_scm\_use\_main\_ip\_restriction) | Should the Linux Web App ip\_restriction configuration be used for the SCM also. | `bool` | `true` | no |
| <a name="input_service_plan_name"></a> [service\_plan\_name](#input\_service\_plan\_name) | The name of the service plan to deploy the web app to | `string` | n/a | yes |
| <a name="input_service_plan_resource_group_name"></a> [service\_plan\_resource\_group\_name](#input\_service\_plan\_resource\_group\_name) | The name of the resource group of the service plan to deploy the web app to | `string` | n/a | yes |
| <a name="input_sticky_settings"></a> [sticky\_settings](#input\_sticky\_settings) | Settings that dont change on slot swap | <pre>object({<br>    app_setting_names       = optional(list(string))<br>    connection_string_names = optional(list(string))<br>  })</pre> | `{}` | no |
| <a name="input_storage_accounts"></a> [storage\_accounts](#input\_storage\_accounts) | Storage accounts to mount | <pre>list(object({<br>    name         = string<br>    access_key   = string<br>    account_name = string<br>    share_name   = string<br>    type         = string<br>    mount_path   = optional(string)<br>  }))</pre> | `[]` | no |
| <a name="input_tags"></a> [tags](#input\_tags) | Tags to apply | `map(string)` | n/a | yes |
| <a name="input_use_32_bit_worker"></a> [use\_32\_bit\_worker](#input\_use\_32\_bit\_worker) | Run on 32-bit worker | `bool` | `false` | no |
| <a name="input_vnet_route_all_enabled"></a> [vnet\_route\_all\_enabled](#input\_vnet\_route\_all\_enabled) | Apply NAT Gateways, Network Security Groups and User Defined Routes to all outbound traffic | `bool` | `true` | no |
| <a name="input_web_app_name"></a> [web\_app\_name](#input\_web\_app\_name) | The name of the web app to deploy | `string` | n/a | yes |
| <a name="input_websockets_enabled"></a> [websockets\_enabled](#input\_websockets\_enabled) | Enable web sockets | `bool` | `false` | no |
| <a name="input_worker_count"></a> [worker\_count](#input\_worker\_count) | The number of Workers | `number` | `null` | no |
| <a name="input_zip_deploy_file"></a> [zip\_deploy\_file](#input\_zip\_deploy\_file) | Local path of zip file to deploy | `string` | `null` | no |

## Outputs

No outputs.
<!-- END_TF_DOCS -->