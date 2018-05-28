VCAP_SERVICES:
```javascript

{
   "VCAP_SERVICES":{
      "xsuaa":[
         {
            "name":"xsuaa-application-jupiter",
            "instance_name":"xsuaa-application-jupiter",
            "binding_name":null,
            "credentials":{
               "uaadomain":"authentication.eu10.hana.ondemand.com",
               "tenantmode":"shared",
               "sburl":"https://internal-xsuaa.authentication.eu10.hana.ondemand.com",
               "clientid":"sb-revenue-cloud!t1532",
               "verificationkey":"-----BEGIN PUBLIC KEY-----MIICIjANBgkqhkiG9w0BAQEFAAOCAg8AMIICCgKCAgEAwThn6OO9kj0bchkOGkqYBnV1dQ3zU/xtj7Kj7nDd8nyRMcEWCtVzrzjzhiisRhlrzlRIEY82wRAZNGKMnw7cvCwNixcfcDJnjzgr2pJ+5/yDZUc0IXXyIWPZD+XdL+0EogC3d4+fqyvg/BF/F0t2hKHWr/UTXE6zrGhBKaL0d8rKfYd6olGWigFd+3+24CKI14zWVxUBtC+P9Fhngc9DRzkXqhxOK/EKn0HzSgotf5duq6Tmk9DCNM4sLW4+ERc6xzrgbeEexakabvax/Az9WZ4qhwgw+fwIhKIC7WLwCEJaRsW4m7NKkv+eJR2LKYesuQ9SVAJ3EXV86RwdnH4uAv7lQHsKURPVAQBlranSqyQu0EXs2N9OlWTxe+FyNkIvyZvoLrZl/CdlYc8AKxRm5rn2/88nkrYQ0XZSrnICM5FRWgVF2hn5KfZGwtBN85/D4Yck6B3ocMfyX7e4URUm9lRPQFUJGTXaZnEIge0R159HUwhTN1HvyXrs6uT1ZZmW+c3p47dw1+LmUf/hIf8zd+uvHQjIeHEJqxjqfyA8yqAFKRHKVFrwnwdMHIsRap2EKBhHMfeVf0P2th5C9MggYoGCvdIaIUgMBX3TtCdvGrcWML7hnyS2zkrlA8SoKJnRcRF2KxWKs355FhpHpzqyZflO5l98+O8wOsFjGpL9d0ECAwEAAQ==-----END PUBLIC KEY-----",
               "xsappname":"revenue-cloud!t1532",
               "identityzone":"revenue-cloud",
               "identityzoneid":"83e252f3-b760-4839-91a3-d0209a3bef0d",
               "clientsecret":"xxxxx-masked-xxxxx",
               "tenantid":"83e252f3-b760-4839-91a3-d0209a3bef0d",
               "url":"https://revenue-cloud.authentication.eu10.hana.ondemand.com"
            },
            "syslog_drain_url":null,
            "volume_mounts":[

            ],
            "label":"xsuaa",
            "provider":null,
            "plan":"application",
            "tags":[
               "xsuaa"
            ]
         },
         {
            "name":"xsuaa-broker-jupiter",
            "instance_name":"xsuaa-broker-jupiter",
            "binding_name":null,
            "credentials":{
               "uaadomain":"authentication.eu10.hana.ondemand.com",
               "trustedclientidsuffix":"|revenue-cloud!b1532",
               "tenantmode":"dedicated",
               "sburl":"https://internal-xsuaa.authentication.eu10.hana.ondemand.com",
               "clientid":"sb-revenue-cloud!b1532",
               "verificationkey":"-----BEGIN PUBLIC KEY-----MIICIjANBgkqhkiG9w0BAQEFAAOCAg8AMIICCgKCAgEAwThn6OO9kj0bchkOGkqYBnV1dQ3zU/xtj7Kj7nDd8nyRMcEWCtVzrzjzhiisRhlrzlRIEY82wRAZNGKMnw7cvCwNixcfcDJnjzgr2pJ+5/yDZUc0IXXyIWPZD+XdL+0EogC3d4+fqyvg/BF/F0t2hKHWr/UTXE6zrGhBKaL0d8rKfYd6olGWigFd+3+24CKI14zWVxUBtC+P9Fhngc9DRzkXqhxOK/EKn0HzSgotf5duq6Tmk9DCNM4sLW4+ERc6xzrgbeEexakabvax/Az9WZ4qhwgw+fwIhKIC7WLwCEJaRsW4m7NKkv+eJR2LKYesuQ9SVAJ3EXV86RwdnH4uAv7lQHsKURPVAQBlranSqyQu0EXs2N9OlWTxe+FyNkIvyZvoLrZl/CdlYc8AKxRm5rn2/88nkrYQ0XZSrnICM5FRWgVF2hn5KfZGwtBN85/D4Yck6B3ocMfyX7e4URUm9lRPQFUJGTXaZnEIge0R159HUwhTN1HvyXrs6uT1ZZmW+c3p47dw1+LmUf/hIf8zd+uvHQjIeHEJqxjqfyA8yqAFKRHKVFrwnwdMHIsRap2EKBhHMfeVf0P2th5C9MggYoGCvdIaIUgMBX3TtCdvGrcWML7hnyS2zkrlA8SoKJnRcRF2KxWKs355FhpHpzqyZflO5l98+O8wOsFjGpL9d0ECAwEAAQ==-----END PUBLIC KEY-----",
               "xsappname":"revenue-cloud!b1532",
               "identityzone":"revenue-cloud",
               "identityzoneid":"83e252f3-b760-4839-91a3-d0209a3bef0d",
               "clientsecret":"xxxxx-masked-xxxxx",
               "tenantid":"83e252f3-b760-4839-91a3-d0209a3bef0d",
               "url":"https://revenue-cloud.authentication.eu10.hana.ondemand.com"
            },
            "syslog_drain_url":null,
            "volume_mounts":[

            ],
            "label":"xsuaa",
            "provider":null,
            "plan":"broker",
            "tags":[
               "xsuaa"
            ]
         }
      ],
      "saas-registry":[
         {
            "name":"saas-registry-application-jupiter",
            "instance_name":"saas-registry-application-jupiter",
            "binding_name":null,
            "credentials":{
               "uaadomain":"authentication.eu10.hana.ondemand.com",
               "tenantmode":"dedicated",
               "sburl":"https://internal-xsuaa.authentication.eu10.hana.ondemand.com",
               "clientid":"sb-revenue-cloud-clone!b1532|lps-registry-broker!b14",
               "verificationkey":"-----BEGIN PUBLIC KEY-----MIICIjANBgkqhkiG9w0BAQEFAAOCAg8AMIICCgKCAgEAwThn6OO9kj0bchkOGkqYBnV1dQ3zU/xtj7Kj7nDd8nyRMcEWCtVzrzjzhiisRhlrzlRIEY82wRAZNGKMnw7cvCwNixcfcDJnjzgr2pJ+5/yDZUc0IXXyIWPZD+XdL+0EogC3d4+fqyvg/BF/F0t2hKHWr/UTXE6zrGhBKaL0d8rKfYd6olGWigFd+3+24CKI14zWVxUBtC+P9Fhngc9DRzkXqhxOK/EKn0HzSgotf5duq6Tmk9DCNM4sLW4+ERc6xzrgbeEexakabvax/Az9WZ4qhwgw+fwIhKIC7WLwCEJaRsW4m7NKkv+eJR2LKYesuQ9SVAJ3EXV86RwdnH4uAv7lQHsKURPVAQBlranSqyQu0EXs2N9OlWTxe+FyNkIvyZvoLrZl/CdlYc8AKxRm5rn2/88nkrYQ0XZSrnICM5FRWgVF2hn5KfZGwtBN85/D4Yck6B3ocMfyX7e4URUm9lRPQFUJGTXaZnEIge0R159HUwhTN1HvyXrs6uT1ZZmW+c3p47dw1+LmUf/hIf8zd+uvHQjIeHEJqxjqfyA8yqAFKRHKVFrwnwdMHIsRap2EKBhHMfeVf0P2th5C9MggYoGCvdIaIUgMBX3TtCdvGrcWML7hnyS2zkrlA8SoKJnRcRF2KxWKs355FhpHpzqyZflO5l98+O8wOsFjGpL9d0ECAwEAAQ==-----END PUBLIC KEY-----",
               "xsappname":"revenue-cloud-clone!b1532|lps-registry-broker!b14",
               "identityzone":"revenue-cloud",
               "identityzoneid":"83e252f3-b760-4839-91a3-d0209a3bef0d",
               "clientsecret":"xxxxx-masked-xxxxx",
               "tenantid":"83e252f3-b760-4839-91a3-d0209a3bef0d",
               "url":"https://revenue-cloud.authentication.eu10.hana.ondemand.com",
               "appName":"revenue-cloud",
               "tenant_onboarding_url":"https://tenant-onboarding.cfapps.eu10.hana.ondemand.com"
            },
            "syslog_drain_url":null,
            "volume_mounts":[

            ],
            "label":"saas-registry",
            "provider":null,
            "plan":"application",
            "tags":[
               "SaaS"
            ]
         },
         {
            "name":"saas-registry-service-jupiter",
            "instance_name":"saas-registry-service-jupiter",
            "binding_name":null,
            "credentials":{
               "appName":"revenue-cloud-api",
               "tenant_onboarding_url":"https://tenant-onboarding.cfapps.eu10.hana.ondemand.com"
            },
            "syslog_drain_url":null,
            "volume_mounts":[

            ],
            "label":"saas-registry",
            "provider":null,
            "plan":"service",
            "tags":[
               "SaaS"
            ]
         }
      ],
      "user-provided":[
         {
            "name":"ups-pdm-jupiter",
            "instance_name":"ups-pdm-jupiter",
            "binding_name":null,
            "credentials":{
               "url":"https://pdm-service.cfapps.eu10.hana.ondemand.com",
               "subscriptionNotificationUri":"/sap/gdprmanager/consumer/onboarding/register/",
               "username":"SBSS_28664931056520857629117734786920956816686538721469162605466243386",
               "password":"xxxxx-masked-xxxxx"
            },
            "syslog_drain_url":"",
            "volume_mounts":[

            ],
            "label":"user-provided",
            "tags":[

            ]
         }
      ],
      "retention-manager":[
         {
            "name":"retention-manager-jupiter",
            "instance_name":"retention-manager-jupiter",
            "binding_name":null,
            "credentials":{
               "vendor":"SAP",
               "applicationSubscription":"https://retention-manager-service.cfapps.eu10.hana.ondemand.com/tenant-application-entitlement/{tenantId}",
               "dataSubjectDeletionEndPoint":"https://retention-manager-service.cfapps.eu10.hana.ondemand.com/retention-constraint-appl",
               "uaa":{
                  "uaadomain":"authentication.eu10.hana.ondemand.com",
                  "tenantmode":"dedicated",
                  "sburl":"https://internal-xsuaa.authentication.eu10.hana.ondemand.com",
                  "clientid":"sb-revenue-cloud!b1532|retention-manager-service!b1824",
                  "verificationkey":"-----BEGIN PUBLIC KEY-----MIICIjANBgkqhkiG9w0BAQEFAAOCAg8AMIICCgKCAgEAwThn6OO9kj0bchkOGkqYBnV1dQ3zU/xtj7Kj7nDd8nyRMcEWCtVzrzjzhiisRhlrzlRIEY82wRAZNGKMnw7cvCwNixcfcDJnjzgr2pJ+5/yDZUc0IXXyIWPZD+XdL+0EogC3d4+fqyvg/BF/F0t2hKHWr/UTXE6zrGhBKaL0d8rKfYd6olGWigFd+3+24CKI14zWVxUBtC+P9Fhngc9DRzkXqhxOK/EKn0HzSgotf5duq6Tmk9DCNM4sLW4+ERc6xzrgbeEexakabvax/Az9WZ4qhwgw+fwIhKIC7WLwCEJaRsW4m7NKkv+eJR2LKYesuQ9SVAJ3EXV86RwdnH4uAv7lQHsKURPVAQBlranSqyQu0EXs2N9OlWTxe+FyNkIvyZvoLrZl/CdlYc8AKxRm5rn2/88nkrYQ0XZSrnICM5FRWgVF2hn5KfZGwtBN85/D4Yck6B3ocMfyX7e4URUm9lRPQFUJGTXaZnEIge0R159HUwhTN1HvyXrs6uT1ZZmW+c3p47dw1+LmUf/hIf8zd+uvHQjIeHEJqxjqfyA8yqAFKRHKVFrwnwdMHIsRap2EKBhHMfeVf0P2th5C9MggYoGCvdIaIUgMBX3TtCdvGrcWML7hnyS2zkrlA8SoKJnRcRF2KxWKs355FhpHpzqyZflO5l98+O8wOsFjGpL9d0ECAwEAAQ==-----END PUBLIC KEY-----",
                  "xsappname":"revenue-cloud!b1532|retention-manager-service!b1824",
                  "identityzone":"revenue-cloud",
                  "identityzoneid":"83e252f3-b760-4839-91a3-d0209a3bef0d",
                  "clientsecret":"xxxxx-masked-xxxxx",
                  "tenantid":"83e252f3-b760-4839-91a3-d0209a3bef0d",
                  "url":"https://revenue-cloud.authentication.eu10.hana.ondemand.com"
               }
            },
            "syslog_drain_url":null,
            "volume_mounts":[

            ],
            "label":"retention-manager",
            "provider":null,
            "plan":"standard",
            "tags":[

            ]
         }
      ],
      "mongodb":[
         {
            "name":"mongodb-jupiter",
            "instance_name":"mongodb-jupiter",
            "binding_name":null,
            "credentials":{
               "uri":"mongodb://b83598352c99cf5361c11d1fd3a7e3df:d43e301e9cc87692d9a8560f0a2267dc@10.11.44.208:27017,10.11.44.209:27017,10.11.44.210:27017/86fa170cba194b04?replicaSet=38760c7a81d00575fc298c55e8008c79",
               "username":"b83598352c99cf5361c11d1fd3a7e3df",
               "password":"xxxxx-masked-xxxxx",
               "dbname":"86fa170cba194b04",
               "port":"27017",
               "replicaset":"38760c7a81d00575fc298c55e8008c79"
            },
            "syslog_drain_url":null,
            "volume_mounts":[

            ],
            "label":"mongodb",
            "provider":null,
            "plan":"v3.0-xsmall",
            "tags":[
               "mongodb",
               "document"
            ]
         }
      ],
      "redis":[
         {
            "name":"redis-jupiter",
            "instance_name":"redis-jupiter",
            "binding_name":null,
            "credentials":{
               "host":"10.11.59.160",
               "hostname":"10.11.59.160",
               "port":"6379",
               "uri":"redis://no-user-name-for-redis:901721296f573263b81f8a6f02e24ad5@10.11.59.160:6379",
               "password":"xxxxx-masked-xxxxx",
               "redis_nodes":[
                  {
                     "hostname":"10.11.59.160",
                     "port":"6379"
                  }
               ]
            },
            "syslog_drain_url":null,
            "volume_mounts":[

            ],
            "label":"redis",
            "provider":null,
            "plan":"v3.0-xsmall-single-node",
            "tags":[
               "redis",
               "keyvalue"
            ]
         }
      ],
      "application-logs":[
         {
            "name":"applogs",
            "instance_name":"applogs",
            "binding_name":null,
            "credentials":{

            },
            "syslog_drain_url":"https://10.0.104.17:4433/syslogv2/ZmVhOTVjMDUtM2RjNi00N2ZlLWJiYTYtZWI0MDdmMDQ5MzhjL2p1cGl0ZXIvMzlkNWM3MzUtOTg4NC00N2U4LWIzYzItMTI5MTI0ZWFkYzZmL2luZnJhc3RydWN0dXJlL2E4ZmE3NjU4LTJjOTctNGFlNS1hNjFiLWEzYTY1NjZiNzcyMi9uZ29tLWluZnJhLWV1MTAvMDVjMmM2NDctZWI2MC00MGI0LWI4YmItNjUxMmEwZWZkNjYyL2FwcGxpY2F0aW9uLWxvZ3MvM2U0NjZmYzYtODMzZS00MzBhLWE1YTEtYjlhYTIzMTk1MGNiL2xhcmdlLzA0OWM2YmNhLTM0MDYtNDc5Zi1hNTE5LTc0NmM3ODA4ZGQyNi9hcHBsb2dzL2IyNjhlN2IxZDY0MjFiMWY1YzJkMTcyMDBkMjE3MWJkNjY3ZDVkMjU4NDIxNWQwNzY2OWUyYzhhMzRjOGFlZDY",
            "volume_mounts":[

            ],
            "label":"application-logs",
            "provider":null,
            "plan":"large",
            "tags":[

            ]
         }
      ],
      "destination":[
         {
            "name":"destinationservice-jupiter",
            "instance_name":"destinationservice-jupiter",
            "binding_name":null,
            "credentials":{
               "uaadomain":"authentication.eu10.hana.ondemand.com",
               "tenantmode":"dedicated",
               "clientid":"sb-clone96762d0aa486410e8a691a950de731cd!b1532|destination-xsappname!b404",
               "instanceid":"96762d0a-a486-410e-8a69-1a950de731cd",
               "verificationkey":"-----BEGIN PUBLIC KEY-----MIICIjANBgkqhkiG9w0BAQEFAAOCAg8AMIICCgKCAgEAwThn6OO9kj0bchkOGkqYBnV1dQ3zU/xtj7Kj7nDd8nyRMcEWCtVzrzjzhiisRhlrzlRIEY82wRAZNGKMnw7cvCwNixcfcDJnjzgr2pJ+5/yDZUc0IXXyIWPZD+XdL+0EogC3d4+fqyvg/BF/F0t2hKHWr/UTXE6zrGhBKaL0d8rKfYd6olGWigFd+3+24CKI14zWVxUBtC+P9Fhngc9DRzkXqhxOK/EKn0HzSgotf5duq6Tmk9DCNM4sLW4+ERc6xzrgbeEexakabvax/Az9WZ4qhwgw+fwIhKIC7WLwCEJaRsW4m7NKkv+eJR2LKYesuQ9SVAJ3EXV86RwdnH4uAv7lQHsKURPVAQBlranSqyQu0EXs2N9OlWTxe+FyNkIvyZvoLrZl/CdlYc8AKxRm5rn2/88nkrYQ0XZSrnICM5FRWgVF2hn5KfZGwtBN85/D4Yck6B3ocMfyX7e4URUm9lRPQFUJGTXaZnEIge0R159HUwhTN1HvyXrs6uT1ZZmW+c3p47dw1+LmUf/hIf8zd+uvHQjIeHEJqxjqfyA8yqAFKRHKVFrwnwdMHIsRap2EKBhHMfeVf0P2th5C9MggYoGCvdIaIUgMBX3TtCdvGrcWML7hnyS2zkrlA8SoKJnRcRF2KxWKs355FhpHpzqyZflO5l98+O8wOsFjGpL9d0ECAwEAAQ==-----END PUBLIC KEY-----",
               "xsappname":"clone96762d0aa486410e8a691a950de731cd!b1532|destination-xsappname!b404",
               "identityzone":"revenue-cloud",
               "clientsecret":"xxxxx-masked-xxxxx",
               "tenantid":"83e252f3-b760-4839-91a3-d0209a3bef0d",
               "uri":"https://destination-configuration.cfapps.eu10.hana.ondemand.com",
               "url":"https://revenue-cloud.authentication.eu10.hana.ondemand.com"
            },
            "syslog_drain_url":null,
            "volume_mounts":[

            ],
            "label":"destination",
            "provider":null,
            "plan":"lite",
            "tags":[
               "destination",
               "document"
            ]
         }
      ]
   }
}
```

VCAP_APPLICATION:
```javascript

{
               "VCAP_APPLICATION": {
                              "cf_api": "https://api.cf.eu10.hana.ondemand.com",
                              "limits": {
                                            "fds": 16384,
                                            "mem": 512,
                                            "disk": 1024
                              },
                              "application_name": "jupiter",
                              "application_uris": [
                                            "eu10.revenue.cloud.sap",
                                            "revenuecloud.cfapps.eu10.hana.ondemand.com",
                                            "*.eu10.revenue.cloud.sap"
                              ],
                              "name": "jupiter",
                              "space_name": "infrastructure",
                              "space_id": "39d5c735-9884-47e8-b3c2-129124eadc6f",
                              "uris": [
                                            "eu10.revenue.cloud.sap",
                                            "revenuecloud.cfapps.eu10.hana.ondemand.com",
                                            "*.eu10.revenue.cloud.sap"
                              ],
                              "users": null,
                              "application_id": "fea95c05-3dc6-47fe-bba6-eb407f04938c",
                              "version": "6299d23e-6eb8-4a01-be7a-717e5732f06d",
                              "application_version": "6299d23e-6eb8-4a01-be7a-717e5732f06d"
               }
}
```
