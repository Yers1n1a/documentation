# aidbox.config/config

<!-- This is autogenerated doc. Source: dev/doc_gen.clj -->

- `:features` (zen/symbol)

  

  zen/tag: [aidbox.config/features](#aidbox.config-features)

- `:bulk-storage` (zen/symbol)

  

  zen/tag: [aidbox.config/bulk-storage](#aidbox.config-bulk-storage)

- `:instance` (zen/map)

  

  - `:name` (zen/string)

    Aidbox instance name using for metrics





- `:compatibility` (zen/symbol)

  

  zen/tag: [aidbox.config/compatibility](#aidbox.config-compatibility)

- `:db` (zen/symbol)

  

  zen/tag: [aidbox.config/db](#aidbox.config-db)

- `:override-createdat-url` (zen/string)

  



- `:debug` (zen/map)

  

  - `:su` (zen/map)

    Allow su header

    - `:enable` (zen/boolean)

      







- `:compliant-mode-enabled?` (zen/boolean)

  



- `:search` (zen/symbol)

  

  zen/tag: [aidbox.config/search](#aidbox.config-search)

- `:auth` (zen/symbol)

  

  zen/tag: [aidbox.config/auth](#aidbox.config-auth)

- `:cache` (zen/map)

  

  - `:replication` (zen/map)

    

    - `:disable` (zen/boolean)

      







- `:replication` (zen/symbol)

  

  zen/tag: [aidbox.config/replication](#aidbox.config-replication)

- `:smartbox` (zen/symbol)

  

  zen/tag: [aidbox.config/smartbox](#aidbox.config-smartbox)

- `:instances-number` (zen/integer)

  



- `:provider` (zen/symbol)

  

  zen/tag: [aidbox.config/provider](#aidbox.config-provider)

- `:fhir-version` (zen/string)

  



- `:metrics` (zen/symbol)

  

  zen/tag: [aidbox.config/metrics](#aidbox.config-metrics)

- `:web` (zen/symbol)

  

  zen/tag: [aidbox.config/web](#aidbox.config-web)

## aidbox.config/features

- `:graphql` (zen/map)

  

  - `:access-control` (zen/string)

    `disabled`: only access to graphql endpoint is verified;
                                                            `rest-search`: additionally authorization checks access to corresponding search queries





- `:validation` (zen/map)

  

  - `:skip` (zen/map)

    Allow skip validation header

    - `:reference` (zen/boolean)

      Allow skip reference validation





  - `:value-set` (zen/map)

    

    - `:mode` (zen/string)

      `disabled`: ignores all value-set binding rules
                                                                  `enabled`: validates value-set binding; only `required` strength bindings are supported now







- `:ftr` (zen/map)

  FTR settings

  - `:pull` (zen/map)

    Ingestion to DB setting

    - `:enable` (zen/boolean)

      Load to Aidbox DB



    - `:sync` (zen/boolean)

      Block Aidbox start







- `:mapping` (zen/map)

  

  - `:enable-access-control` (zen/boolean)

    `false`: only access to $apply endpoints are verified
                                                                   `true`: enable access control for resulting transaction





- `:authentication` (zen/map)

  

  - `:skip-jwt-validation` (zen/boolean)

    



  - `:introspection` (zen/map)

    

    - `:create-user` (zen/boolean)

      create a user when not exists and JWT is valid





  - `:auth-with-not-validated-jwt` (zen/any)

    





- `:http` (zen/map)

  

  - `:return-404-on-empty-delete` (zen/boolean)

    Return 404 HTTP code when no resources are deleted.





- `:terminology` (zen/map)

  

  - `:import` (zen/map)

    

    - `:sync` (zen/boolean)

      







## aidbox.config/bulk-storage

- `:backend` (zen/string)

  



- `:gcp` (zen/map)

  

  - `:service-account` (zen/string)

    



  - `:bucket` (zen/string)

    





- `:aws` (zen/map)

  

  - `:account` (zen/string)

    



  - `:bucket` (zen/string)

    





- `:azure` (zen/map)

  

  - `:container` (zen/string)

    





## aidbox.config/compatibility

- `:validation` (zen/map)

  

  - `:json-schema` (zen/map)

    

    - `:regex` (zen/any)

      







- `:auth` (zen/map)

  

  - `:pkce` (zen/map)

    

    - `:code-challenge` (zen/map)

      

      - `:s256` (zen/map)

        

        - `:conformant` (zen/boolean)

          RFC-conformant code challenge validation











## aidbox.config/db

- `:pool` (zen/map)

  

  - `:connection-timeout` (zen/integer)

    ms



  - `:idle-timeout` (zen/integer)

    ms



  - `:minimum-idle` (zen/integer)

    



  - `:maximum-pool-size` (zen/integer)

    



  - `:connection-init-sql` (zen/string)

    





- `:database` (zen/string)

  



- `:host` (zen/string)

  



- `:port` (zen/string)

  



- `:user` (zen/string)

  



- `:password` (zen/string)

  



## aidbox.config/search

- `:zen-fhir` (zen/keyword)

  



- `:fhir-comparisons` (zen/boolean)

  Use FHIR compliant comparisons in search instead of legacy Aidbox comparisons. This affects searching with prefixes, e.g. gt2020



- `:default-params` (zen/map)

  

  - `:timeout` (zen/integer)

    default timeout value (seconds). also uses at timeout to the `count` query



  - `:total` (zen/string)

    



  - `:count` (zen/integer)

    default count value





- `:chain` (zen/map)

  

  - `:subselect` (zen/boolean)

    Use subselect for simple forward chain searches. That is only one chain which doesn't contain intermediate hops.





## aidbox.config/auth

- `:grant-page-url` (zen/string)

  



- `:login-redirect` (zen/string)

  



- `:keys` (zen/map)

  

  - `:private` (zen/string)

    



  - `:public` (zen/string)

    



  - `:secret` (zen/string)

    





## aidbox.config/replication

- `:instances` (zen/integer)

  



- `:port` (zen/integer)

  



- `:kube` (zen/map)

  Kubernetes meta

  - `:service-name` (zen/string)

    



  - `:namespace` (zen/string)

    Kubernetes namespace



  - `:hostname` (zen/string)

    Kubernetes hostname. Deduce instance number





## aidbox.config/smartbox

- `:sandbox-url` (zen/string)

  



- `:sandbox-basic` (zen/string)

  



- `:session-logs-link` (zen/string)

  



## aidbox.config/provider

- `:default` (zen/map)

  

  - `:ssl` (zen/boolean)

    



  - `:password` (zen/string)

    



  - `:username` (zen/string)

    



  - `:type` (zen/string)

    



  - `:tls` (zen/boolean)

    



  - `:port` (zen/integer)

    



  - `:host` (zen/string)

    



  - `:from` (zen/string)

    



  - `:url` (zen/string)

    



  - `:api-key` (zen/string)

    





- `:mailgun-provider` (zen/map)

  

  - `:type` (zen/string)

    



  - `:from` (zen/string)

    



  - `:username` (zen/string)

    



  - `:password` (zen/string)

    



  - `:url` (zen/string)

    





- `:postmark-provider` (zen/map)

  

  - `:type` (zen/string)

    



  - `:from` (zen/string)

    



  - `:api-key` (zen/string)

    





## aidbox.config/metrics

- `:postgres` (zen/map)

  

  - `:on` (zen/boolean)

    Enable/disable postgres metrics





- `:port` (zen/integer)

  Metrics server port



- `:grafana` (zen/map)

  Connection to grafana to update the metrics dashboards

  - `:user` (zen/string)

    



  - `:password` (zen/string)

    



  - `:url` (zen/string)

    





## aidbox.config/web

- `:port` (zen/integer)

  



- `:thread` (zen/integer)

  



- `:max-body` (zen/integer)

  



- `:request-save-raw-body` (zen/boolean)

  Attach raw body to response




