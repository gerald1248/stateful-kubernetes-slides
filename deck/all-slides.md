<!-- section 0 -->

# STATEFUL KUBERNETES {#stateful-kubernetes .light-on-dark bgcss="tw-colorful"}

`<smaller>`{=html}PAST, PRESENT, FUTURE`</smaller>`{=html}

<!-- section 1 -->

# STATELESS KUBERNETES {#stateless-kubernetes bg="#97dce7"}

``` {.render_a2sketch}
                      #------------#
                      |[c]         |
                      |  Users     |
                      |            |
                      #-----#------#
                            |
                            v
                      #-----#------#
                      |[o]         |
                      | Service    | service.namespace.svc.cluster.local
                      |            |
                      #-----#------#
                            |
             #--------------#--------------#
             |                             |
             v              |              v
#------------#------------.   #------------#------------.
|[p]                      | | |[p]                      |
| Pod                     |   | Pod                     |
|                         | | |                         |
#------------#------------.   #------------#------------#
|[w]         |[w]         | | |[w]         |[w]         |
| Container  | Container  |   | Container  | Container  |
|            |            | | |            |            |
#------------#------------#   #------------#------------#
|[w]                      | | |[w]                      |
| Host                    |   | Host                    |
| [zone=a]                | | | [zone=b]                |
'-------------------------#   '-------------------------#
                            |                           
Availability zone a           Availability zone b      
                            |

[c]: {"a2s:type": "cloud", "a2s:delref": true, "fill": "#fff", "fillStyle": "solid"}
[w]: {"a2s:delref": true, "fill": "#fff", "fillStyle": "solid", "strokeStyle": "#000"}
[g]: {"a2s:delref": true, "fill": "transparent", "fillStyle": "solid", "strokeStyle": "#000"}
[p]: {"a2s:delref": true, "fill": "#ef5ba1", "fillStyle": "solid", "strokeStyle": "#000"}
[o]: {"a2s:delref": true, "fill": "#f99c41", "fillStyle": "solid"}
```

<!-- section 2 -->

# CONTAINER STORAGE FABLE {#container-storage-fable bg="#97dce7"}

``` {.render_a2sketch}
                      #------------#
                      |[c]         |
                      |  Users     |
                      |            |
                      #-----#------#
                            |
                            v
                      #-----#------#
                      |[o]         |
                      | Service    |
                      |            |
                      #-----#------#
                            |
             #--------------#--------------#
             |                             |
             v              |              v
#------------#------------.   #------------#------------.
|[p]                      | | |[p]                      |
| Pod                     |   | Pod                     |
|                         | | |                         |
#-------------------------.   #-------------------------#
|[w]                      | | |[w]                      |
| Container    .----------#   | Container    .----------#
|              |[e] Store | | |              |[e] Store |  <-- That's NOT
#--------------#----------#   #--------------#----------#      how this works
|[w]                      | | |[w]                      |
| Host                    |   | Host                    |
| [zone=a]                | | | [zone=b]                |
'-------------------------#   '-------------------------#
                            |                           
Availability zone a           Availability zone b      
                            |

[c]: {"a2s:type": "cloud", "a2s:delref": true, "fill": "#fff", "fillStyle": "solid"}
[w]: {"a2s:delref": true, "fill": "#fff", "fillStyle": "solid", "strokeStyle": "#000"}
[g]: {"a2s:delref": true, "fill": "transparent", "fillStyle": "solid", "strokeStyle": "#000"}
[p]: {"a2s:delref": true, "fill": "#ef5ba1", "fillStyle": "solid", "strokeStyle": "#000"}
[o]: {"a2s:delref": true, "fill": "#f99c41", "fillStyle": "solid"}
[e]: {"a2s:delref": true, "fill": "#00aa5b", "fillStyle": "solid", "strokeStyle": "#000"}
```

<!-- section 3 -->

# CONTAINER BLOCK STORAGE {#container-block-storage bg="#97dce7"}

``` {.render_a2sketch}
                      #------------#
                      |[c]         |
                      |  Users     |
                      |            |
                      #-----#------#
                            |
                            v
                      #-----#------#
                      |[o]         |
                      | Service    |
                      |            |                       #-------------#
                      #-----#------#                       |[w]          |
                            |                        .----># PVC         |
             #--------------#--------------#         |     | (namespace) |
             |                             |         |     #-------#-----#
             v              |              v         |             |
#------------#------------.   #------------#---------#--.          v
|[p]                      | | |[p]                      |  #-------#-----#
| Pod                     |   | Pod                     |  |[w]          |
|                         | | |                         |  | PV          |
#------------#------------.   #------------#------------#  | (cluster)   |
|[w]         |[w]         | | |[w]         |[w]         |  #-------#-----#
| Container  | Container  |   | Container  | Container  |          |
|            |            | | |            |            |          |
#------------#------------#   #------------#------------#          |
|[w]                      | | |[w]                      |          |
| Host          .---------#   | Host          .---------#          |
| [zone=a]      |[e]Drive | | | [zone=b]      |[e]Drive |          |
'---------------#---------#   '---------------#------#--#          |
                            |                        ^             | 
Availability zone a           Availability zone b    |             |
                                                     '-------------'
                                                        mount RWO
[c]: {"a2s:type": "cloud", "a2s:delref": true, "fill": "#fff", "fillStyle": "solid"}
[w]: {"a2s:delref": true, "fill": "#fff", "fillStyle": "solid", "strokeStyle": "#000"}
[g]: {"a2s:delref": true, "fill": "transparent", "fillStyle": "solid", "strokeStyle": "#000"}
[p]: {"a2s:delref": true, "fill": "#ef5ba1", "fillStyle": "solid", "strokeStyle": "#000"}
[o]: {"a2s:delref": true, "fill": "#f99c41", "fillStyle": "solid"}
[e]: {"a2s:delref": true, "fill": "#00aa5b", "fillStyle": "solid", "strokeStyle": "#000"}
```

<!-- section 4 -->

# CONTAINER NETWORK FILE STORAGE {#container-network-file-storage bg="#97dce7"}

``` {.render_a2sketch}
                      #------------#
                      |[c]         |
                      |  Users     |
                      |            |
                      #-----#------#
                            |
                            v
                      #-----#------#
                      |[o]         |
                      | Service    |
                      |            |                       #-------------#
                      #-----#------#                       |[w]          |
                            |                        .----># PVC         |
             #--------------#--------------#         |     | (namespace) |
             |                             |         |     #-------#-----#
             v              |              v         |             |
#------------#------------.   #------------#---------#--.          v
|[p]                      | | |[p]                      |  #-------#-----#
| Pod                     |   | Pod                     |  |[w]          |
|                         | | |                         |  | PV          |
#------------#------------.   #------------#------------#  | (cluster)   |
|[w]         |[w]         | | |[w]         |[w]         |  #-------#-----#
| Container  | Container  |   | Container  | Container  |          |
|            |            | | |            |            |          v
#------------#------------#   #------------#------------#  #-------#-----#
|[w]                      | | |[w]                      |  |[e]          |
| Host                    |   | Host                    |  | NFS         |   
| [zone=a]                | | | [zone=b]                |  |             |
'----------------------#--#   '----------------------#--#  #-------#-----#
                       ^    |                        ^             | 
Availability zone a    |      Availability zone b    |             |
                       '-----------------------------#-------------'
                                             mount RWX
[c]: {"a2s:type": "cloud", "a2s:delref": true, "fill": "#fff", "fillStyle": "solid"}
[w]: {"a2s:delref": true, "fill": "#fff", "fillStyle": "solid", "strokeStyle": "#000"}
[g]: {"a2s:delref": true, "fill": "transparent", "fillStyle": "solid", "strokeStyle": "#000"}
[p]: {"a2s:delref": true, "fill": "#ef5ba1", "fillStyle": "solid", "strokeStyle": "#000"}
[o]: {"a2s:delref": true, "fill": "#f99c41", "fillStyle": "solid"}
[e]: {"a2s:delref": true, "fill": "#00aa5b", "fillStyle": "solid", "strokeStyle": "#000"}
```

<!-- section 5 -->

# TIMELINES {#timelines .light-on-dark bg="#6a2469"}

`<smaller>`{=html}IDENTITY, NETWORK, STORAGE AND STATE`</smaller>`{=html}

<!-- section 6 -->

# IDENTITY {#identity bg="#97dce7"}

``` {.render_plantuml args="-Sbackgroundcolor=transparent"}
@startuml
skinparam BoxPadding 10
skinparam defaultFontSize 18
Kubernetes->OpenShift : attribute-based access control (ABAC)
OpenShift->Kubernetes : roles and cluster-roles
Kubernetes->OpenShift : role-based access control (RBAC)
@enduml
```

```{=html}
<aside class="notes" data-markdown>
```
Since Red Hat embraced Kubernetes for OpenShift 3+, there have been numerous virtuous pizza effects, large and small. RBAC is an example that has worked particularly well.
```{=html}
</aside>
```
<!-- section 7 -->

# NETWORK {#network bg="#97dce7"}

``` {.render_plantuml args="-Sbackgroundcolor=transparent"}
@startuml
skinparam BoxPadding 10
skinparam defaultFontSize 18
Kubernetes->OpenShift : flat network
OpenShift->Kubernetes : multitenant plugin
OpenShift->Kubernetes : prototype network policies
Kubernetes->OpenShift : network policies
@enduml
```

```{=html}
<aside class="notes" data-markdown>
```
Network policies have arguably been less successful. The question is whether network policies warrant the considerable amount of complexity when placed alongside Red Hat's original `ovs-multitenant` plugin.
```{=html}
</aside>
```
<!-- section 8 -->

# STORAGE AND STATE {#storage-and-state bg="#97dce7"}

``` {.render_plantuml args="-Sbackgroundcolor=transparent"}
@startuml
skinparam BoxPadding 10
skinparam defaultFontSize 18
Kubernetes->"Red Hat OpenShift" : beware stateful applications
"Red Hat OpenShift"->Kubernetes : application templates (2015)
Kubernetes->"CoreOS Tectonic" : stateful applications still hard
"CoreOS Tectonic"->Kubernetes : etcd operator with third-party resources (2016)
Kubernetes->"CoreOS Tectonic" : Custom Resource Definitions
"CoreOS Tectonic"->Kubernetes : Operator Framework and SDK (2018)
"CoreOS Tectonic"->"Red Hat OpenShift" : merges with (2019)
@enduml
```

<!-- section 9 -->

# REBUILDING THE DATACENTRE {#rebuilding-the-datacentre bg="#97dce7"}

``` {.render_a2sketch}
.--------------------------------------------------------------------------------------#
|[p]                                                                                   |
|                                     Kubernetes                                       |
|                                                                                      |
#--------------------------------------------------------------------------------------#
|[b]                                                                                   |
|                             Role-based access control                                |
|                                                                                      |
#----------------------------#----------------------------#----------------------------#
|[d]                         |[d]                         |[e]                         |
|Container runtime interface |Container network interface |Container storage interface |
|                            |                            |                            |
#----------------------------#----------------------------#----------------------------#

[c]: {"a2s:delref": true, "fill": "#fff", "fillStyle": "solid"}
[p]: {"a2s:delref": true, "fill": "#ef5ba1", "fillStyle": "solid", "strokeStyle": "#000"}
[b]: {"a2s:delref": true, "fill": "#f99c41", "fillStyle": "solid", "strokeStyle": "#000"}
[d]: {"a2s:delref": true, "fill": "#27bdce", "fillStyle": "solid", "strokeStyle": "#000"}
[e]: {"a2s:delref": true, "fill": "#00aa5b", "fillStyle": "solid", "strokeStyle": "#000"}
[t]: {"a2s:delref": true, "fill": "transparent", "fillStyle": "solid", "strokeStyle": "#000"}
[w]: {"a2s:delref": true, "fill": "#fff", "fillStyle": "solid", "strokeStyle": "#000"}
[db]: {"a2s:delref": true, "fill": "#1e8490", "fillStyle": "solid", "strokeStyle": "#000"}
```

<!-- section 10 -->

# ECOSYSTEM RESILIENCE {#ecosystem-resilience .light-on-dark bg="#6a2469"}

<!-- section 11 -->

# SHARED OWNERSHIP {#shared-ownership bg="#97dce7"}

``` {.render_a2sketch}
.-----------------------------------------------------------.
|[t]                                                        |
| #-------------------------#   #-------------------------# |     
| |[p]                      |   |[b]                      | |    
| |                         |   |        IBM              | |    
| |      Microsoft          |   |        Red Hat          | |     
| |                         |   |        CoreOS           | |    
| |                         |   |                         | |    
| #-------------------------#   #-------------------------# |     
|                                                           |
|           #----------------------------------#            |
|           |[c]                               |            |
|           |                                  |            |
|           |              Google              |            |
|           |                                  |            |
|           |                                  |            |
|           #----------------------------------#            |
|                                                           |
| #-------------------------#   #-------------------------# |     
| |[d]                      |   |[e]                      | |    
| |                         |   |                         | |     
| |        VMware           |   |        Alibaba          | |      
| |                         |   |                         | |     
| |                         |   |                         | |     
| #-------------------------#   #-------------------------# |     
|                                                           |
|          Cloud Native Computing Foundation (CNCF)         |
|                                                           |
'-----------------------------------------------------------'
 
[c]: {"a2s:delref": true, "fill": "#fff", "fillStyle": "solid"}
[p]: {"a2s:delref": true, "fill": "#ef5ba1", "fillStyle": "solid", "strokeStyle": "#000"}
[b]: {"a2s:delref": true, "fill": "#f99c41", "fillStyle": "solid", "strokeStyle": "#000"}
[d]: {"a2s:delref": true, "fill": "#27bdce", "fillStyle": "solid", "strokeStyle": "#000"}
[e]: {"a2s:delref": true, "fill": "#00aa5b", "fillStyle": "solid", "strokeStyle": "#000"}
[t]: {"a2s:delref": true, "fill": "transparent", "fillStyle": "solid", "strokeStyle": "#000"}
```

<!-- section 12 -->

# PRECONDITIONS {#preconditions bg="#97dce7"}

``` {.render_a2sketch}
.---------------------------------------------------#
|[w]                                                |
| open source                                       |
|                                                   |
#---------------------------------------------------#
|[w]                                                |
| neutral IP ownership                              |
|                                                   |
#---------------------------------------------------#
|[w]                                                |
| extensibility                                     |
|                                                   |
#---------------------------------------------------'

[w]: {"a2s:delref": true, "fill": "#fff", "fillStyle": "solid"}
[p]: {"a2s:delref": true, "fill": "#ef5ba1", "fillStyle": "solid", "strokeStyle": "#000"}
[b]: {"a2s:delref": true, "fill": "#f99c41", "fillStyle": "solid", "strokeStyle": "#000"}
[d]: {"a2s:delref": true, "fill": "#27bdce", "fillStyle": "solid", "strokeStyle": "#000"}
[e]: {"a2s:delref": true, "fill": "#00aa5b", "fillStyle": "solid", "strokeStyle": "#000"}

```

<!-- section 13 -->

# PRECONDITIONS {#preconditions-1 bg="#97dce7"}

``` {.render_a2sketch}
.---------------------------------------------------#
|[p]                                                |
| open source - Apache                              |
|                                                   |
#---------------------------------------------------#
|[w]                                                |
| neutral IP ownership                              |
|                                                   |
#---------------------------------------------------#
|[w]                                                |
| extensibility                                     |
|                                                   |
#---------------------------------------------------'

[w]: {"a2s:delref": true, "fill": "#fff", "fillStyle": "solid"}
[p]: {"a2s:delref": true, "fill": "#ef5ba1", "fillStyle": "solid", "strokeStyle": "#000"}
[b]: {"a2s:delref": true, "fill": "#f99c41", "fillStyle": "solid", "strokeStyle": "#000"}
[d]: {"a2s:delref": true, "fill": "#27bdce", "fillStyle": "solid", "strokeStyle": "#000"}
[e]: {"a2s:delref": true, "fill": "#00aa5b", "fillStyle": "solid", "strokeStyle": "#000"}
```

A suitably permissive license is a necessary but not sufficient precondition.

<!-- section 14 -->

# PRECONDITIONS {#preconditions-2 bg="#97dce7"}

``` {.render_a2sketch}
.---------------------------------------------------#
|[p]                                                |
| open source - Apache                              |
|                                                   |
#---------------------------------------------------#
|[b]                                                |
| neutral IP ownership - CNCF                       |
|                                                   |
#---------------------------------------------------#
|[w]                                                |
| extensibility                                     |
|                                                   |
#---------------------------------------------------'

[w]: {"a2s:delref": true, "fill": "#fff", "fillStyle": "solid"}
[p]: {"a2s:delref": true, "fill": "#ef5ba1", "fillStyle": "solid", "strokeStyle": "#000"}
[b]: {"a2s:delref": true, "fill": "#f99c41", "fillStyle": "solid", "strokeStyle": "#000"}
[d]: {"a2s:delref": true, "fill": "#27bdce", "fillStyle": "solid", "strokeStyle": "#000"}
[e]: {"a2s:delref": true, "fill": "#00aa5b", "fillStyle": "solid", "strokeStyle": "#000"}
```

<!-- section 15 -->

# PRECONDITIONS {#preconditions-3 bg="#97dce7"}

``` {.render_a2sketch}
#---------------------------------------------------#
|[q]                                                |
|                                                   |
|                                                   |
|                                                   |
| K8s would *not* be what it is today without       |
|                                                   |
| neutral IP ownership... K8s has spawned an entire |
|                                                   |
| ecosystem *because* it can be used by consuming   |
|                                                   |
| projects/products without fear.                   |
|                                                   |
|                             - Matt Klein          |
|                                                   |
|                                                   |
|                                                   |
|                                                   |
#---------------------------------------------------#
[q]: {"a2s:type": "quote-sw", "a2s:delref": true, "fill": "#f99c41", "fillStyle": "solid"}
```

::: {.tiny}
Source: `<a href="https://twitter.com/mattklein123/status/1229513052673855488?ref_src=twsrc%5Etfw">`{=html}@mattklein123 on Twitter`</a>`{=html}, 17 February 2020.
:::

<!-- section 16 -->

# PRECONDITIONS {#preconditions-4 bg="#97dce7"}

``` {.render_a2sketch}
.---------------------------------------------------#
|[p]                                                |
| open source - Apache                              |
|                                                   |
#---------------------------------------------------#
|[b]                                                |
| neutral IP ownership - CNCF                       |
|                                                   |
#---------------------------------------------------#
|[d]                                                |
| extensibility - controllers and operators         |
|                                                   |
#---------------------------------------------------'

[w]: {"a2s:delref": true, "fill": "#fff", "fillStyle": "solid"}
[p]: {"a2s:delref": true, "fill": "#ef5ba1", "fillStyle": "solid", "strokeStyle": "#000"}
[b]: {"a2s:delref": true, "fill": "#f99c41", "fillStyle": "solid", "strokeStyle": "#000"}
[d]: {"a2s:delref": true, "fill": "#27bdce", "fillStyle": "solid", "strokeStyle": "#000"}
[e]: {"a2s:delref": true, "fill": "#00aa5b", "fillStyle": "solid", "strokeStyle": "#000"}
```

**Controllers** add custom processing to the core reconciliation loop.

When paired with custom resource definitions, they are known as **operators**.

<!-- section 17 -->

# THE OPERATOR LIFE {#the-operator-life .light-on-dark bg="#6a2469"}

<!-- section 18 -->

# OPERATORS {#operators bg="#fff44d"}

``` {.render_a2sketch}
#--------------------------#     #-------------------------#       
|[p]                       |     |[b]                      |      
|                          |     |                         |      
|                          |     |                         |      
|Custom Resource Definition+--+--+        Controller       |       
|                          |  |  |                         |      
|  (e.g. "VaultService")   |  |  | (backup, upgrade, etc.) |      
|                          |  |  |                         |      
|                          |  |  |                         |      
#--------------------------#  |  #-------------------------#       
                              |
                              |
                              v
                 #------------+-------------#  
                 |[s]                       | 
                 |                          | 
                 |                          |  
                 |                          | 
                 |                          | 
                 |   Cluster state (etcd)   |  
                 |                          | 
                 |    PersistentVolumes     |  
                 |                          | 
                 |        ConfigMaps        |  
                 |                          | 
                 |          Secrets         |  
                 #--------------------------#  


[p]: {"a2s:delref": true, "fill": "#ef5ba1", "fillStyle": "solid", "strokeStyle": "#000"}
[b]: {"a2s:delref": true, "fill": "#f99c41", "fillStyle": "solid", "strokeStyle": "#000"}
[s]: {"a2s:type":"storage", "a2s:delref": true, "fillStyle": "solid", "fill": "#ffffff"}
```

<!-- section 19 -->

# CORPORATE SPONSORS {#corporate-sponsors bg="#fff44d"}

Vault operator`<br/>`{=html}
`<img src="assets/img/CoreOS.svg" width="200px"/>`{=html}

MySQL operator`<br/>`{=html}
`<img src="assets/img/Oracle_logo.svg" width="200px"/>`{=html}

PostgreSQL operator`<br/>`{=html}
`<img src="assets/img/Zalando_logo.svg" width="200px"/>`{=html}

<!-- section 20 -->

# STATEFUL WORKLOADS {#stateful-workloads bg="#97dce7"}

``` {.render_a2sketch}
#------------------------------------------------------------------#
|[q]                                                               |
|                                                                  |
|                                                                  |
|                                                                  |
|    Stateless is Easy, Stateful is Hard.                          |
|                                                                  |
|                                   - Brandon Philips (2016)       |
|                                                                  |
|                                                                  |
|                                                                  |
#------------------------------------------------------------------#

[q]: {"a2s:type": "quote-sw", "a2s:delref": true, "fill": "#ef5ba1", "fillStyle": "solid"}
```

::: {.tiny}
Source: `<a href="https://coreos.com/blog/introducing-operators.html">`{=html}coreos.com/blog/introducing-operators.html`</a>`{=html}
:::

<!-- section 21 -->

# SOUL-SEARCHING AT THE BAZAAR {#soul-searching-at-the-bazaar .light-on-dark bg="#6a2469"}

<!-- section 22 -->

# FALLING OUT OVER STATE MANAGEMENT {#falling-out-over-state-management bg="#97dce7"}

``` {.render_a2sketch}
     #-----------------------------------------------------------#
     |[w]                                                        |
     | #-------------------------#   #-------------------------# |      
     | |[p]                      |   |[b]                      | |    
     | |     Azure Key Vault     |   |       Cosmos DB         | |     
     | |                         |   |                         | |    
     | #-------------------------#   #-------------------------# |     
     |           #----------------------------------#            |
     |           |[w]                               |            |
     |           |              AKS                 |            |
     |           |                                  |            |
     |           #----------------------------------#            |
     | #-------------------------#   #-------------------------# |     
     | |[d]                      |   |[e]                      | |    
     | |      Azure DevOps       |   |   Azure Queue Storage   | |      
     | |                         |   |                         | |     
     | #-------------------------#   #-------------------------# |     
     |                           Azure                           |     
     #-----------------------------#-----------------------------#     

[w]: {"a2s:delref": true, "fill": "#fff", "fillStyle": "solid"}
[p]: {"a2s:delref": true, "fill": "#ef5ba1", "fillStyle": "solid", "strokeStyle": "#000"}
[b]: {"a2s:delref": true, "fill": "#f99c41", "fillStyle": "solid", "strokeStyle": "#000"}
[d]: {"a2s:delref": true, "fill": "#27bdce", "fillStyle": "solid", "strokeStyle": "#000"}
[e]: {"a2s:delref": true, "fill": "#00aa5b", "fillStyle": "solid", "strokeStyle": "#000"}
```

Cloud vendors perfected the use of proprietary services based on open source products, putting companies creating those products on notice.

In 2016 MongoDB Inc. responded with the `<a href="https://www.mongodb.com/community/licensing">`{=html}Server Side Public License`</a>`{=html}.

<!-- section 23 -->

# A PORTABLE STACK {#a-portable-stack bg="#97dce7"}

``` {.render_a2sketch}
  
     #-----------------------------#-----------------------------#
     |[w]                                                        |
     | #-------------------------#   #-------------------------# |      
     | |[p]                      |   |[b]                      | |    
     | |     Vault operator      |   |   PostgreSQL operator   | |     
     | |                         |   |                         | |    
     | #-------------------------#   #-------------------------# |     
     |                                                           |    
     | #-------------------------#   #-------------------------# |     
     | |[d]                      |   |[e]                      | |    
     | |       Jenkins X         |   |     Kafka operator      | |      
     | |                         |   |                         | |     
     | #-------------------------#   #-------------------------# |     
     |                Any managed Kubernetes service             |     
     #-----------------------------------------------------------#     

[w]: {"a2s:delref": true, "fill": "#fff", "fillStyle": "solid"}
[p]: {"a2s:delref": true, "fill": "#ef5ba1", "fillStyle": "solid", "strokeStyle": "#000"}
[b]: {"a2s:delref": true, "fill": "#f99c41", "fillStyle": "solid", "strokeStyle": "#000"}
[d]: {"a2s:delref": true, "fill": "#27bdce", "fillStyle": "solid", "strokeStyle": "#000"}
[e]: {"a2s:delref": true, "fill": "#00aa5b", "fillStyle": "solid", "strokeStyle": "#000"}
```

<!-- section 24 -->

# INFRASTRUCTURE AS ~~CODE~~DATA {#infrastructure-as-codedata bg="#97dce7"}

``` {.render_a2sketch}
#-----------------------------------------------------------------#
|[q]                                                              |
|                                                                 |
|                                                                 |
|                                                                 |
|  Declarative configuration is about treating infrastructure as  |
|                                                                 |
|  data, which is more portable than code, and enables workflows  |
|                                                                 |
|  that manipulate desired state based on policy.                 |
|                                                                 |
|                                   - Kelsey Hightower (2019)     |
|                                                                 |
|                                                                 |
|                                                                 |
#-----------------------------------------------------------------#

[q]: {"a2s:type": "quote-sw", "a2s:delref": true, "fill": "#ef5ba1", "fillStyle": "solid"}
```

::: {.tiny}
Source: `<a href="https://twitter.com/kelseyhightower/status/1164194470436302848">`{=html}@kelseyhightower on Twitter, 21 August 2019`</a>`{=html}.
:::

<!-- section 25 -->

# DESIRED STATE {#desired-state bg="#97dce7"}

``` {.render_a2sketch}
     #-----------------------------------------------------------#                  -#         
     |[w]                                                        |                   |   
     | #-------------------------#   #-------------------------# |                   |   
     | |[p]                      |   |[b]                      | |                   #----------.
     | |     Azure Key Vault     |   |       Cosmos DB         | |                   |          |
     | |                         |   |                         | |                   |          |
     | #-------------------------#   #-------------------------# |                  -#          |
     |           #----------------------------------#            |              -#              |
     |           |[w]                               |            |               |        plan, |
     |           |              AKS                 |            | reconciliation|       apply, |
     |           |                                  |            |     loop      |   save state |
     |           #----------------------------------#            |              -#              |
     | #-------------------------#   #-------------------------# |                  -#          |
     | |[d]                      |   |[e]                      | |                   |          |
     | |      Azure DevOps       |   |   Azure Queue Storage   | |                   |          |
     | |                         |   |                         | |                   #----------'
     | #-------------------------#   #-------------------------# |                   |   
     |                           Azure                           |                   |   
     #-----------------------------#-----------------------------#                  -#   
            Infrastructure as CODE | 
                                   |
                                   |
                                   |
                                   v Infrastructure as DATA                          -#
     #-----------------------------#-----------------------------#                    #---------.
     |[w]                                                        |                   -#         |
     | #-------------------------#   #-------------------------# |              -#              |
     | |[p]                      |   |[b]                      | |               |              |
     | |     Vault operator      |   |   PostgreSQL operator   | |               |              |
     | |                         |   |                         | |               |              |
     | #-------------------------#   #-------------------------# |               |        plan, |
     |                                                           | reconciliation|       apply, |
     | #-------------------------#   #-------------------------# |     loop      |   save state |
     | |[d]                      |   |[e]                      | |               |              |
     | |       Jenkins X         |   |     Kafka operator      | |               |              |
     | |                         |   |                         | |               |              |
     | #-------------------------#   #-------------------------# |              -#              |
     |                Any managed Kubernetes service             |                   -#         | 
     #-----------------------------------------------------------#                    #---------' 
                                                                                     -#

[w]: {"a2s:delref": true, "fill": "#fff", "fillStyle": "solid"}
[p]: {"a2s:delref": true, "fill": "#ef5ba1", "fillStyle": "solid", "strokeStyle": "#000"}
[b]: {"a2s:delref": true, "fill": "#f99c41", "fillStyle": "solid", "strokeStyle": "#000"}
[d]: {"a2s:delref": true, "fill": "#27bdce", "fillStyle": "solid", "strokeStyle": "#000"}
[e]: {"a2s:delref": true, "fill": "#00aa5b", "fillStyle": "solid", "strokeStyle": "#000"}
```

```{=html}
<aside class="notes" data-markdown>
```
```{=html}
</aside>
```
<!-- section 26 -->

# TRADE-OFFS {#trade-offs bg="#97dce7"}

``` {.render_a2sketch}
     #-----------------------------------------------------------#                  -#         
     |[w]                                                        |                   |   
     | #-------------------------#   #-------------------------# |                   |   
     | |[p]                      |   |[b]                      | |                   #----------.
     | |     Azure Key Vault     |   |       Cosmos DB         | |                   |          |
     | |                         |   |                         | |                   |          |
     | #-------------------------#   #-------------------------# |                  -#          |
     |           #----------------------------------#            |              -#              |
     |           |[w]                               |            |    open source|  proprietary |
     |           |              AKS                 |            |    less sticky|       sticky |
     |           |                                  |            |    less mature|       mature |
     |           #----------------------------------#            |              -#              |
     | #-------------------------#   #-------------------------# |                  -#          |
     | |[d]                      |   |[e]                      | |                   |          |
     | |      Azure DevOps       |   |   Azure Queue Storage   | |                   |          |
     | |                         |   |                         | |                   #----------'
     | #-------------------------#   #-------------------------# |                   |   
     |                           Azure                           |                   |   
     #-----------------------------#-----------------------------#                  -#   
            Infrastructure as CODE | 
                                   |
                                   |
                                   |
                                   v Infrastructure as DATA                          -#
     #-----------------------------#-----------------------------#                    #---------.
     |[w]                                                        |                   -#         |
     | #-------------------------#   #-------------------------# |              -#              |
     | |[p]                      |   |[b]                      | |               |              |
     | |     Vault operator      |   |   PostgreSQL operator   | |               |              |
     | |                         |   |                         | |               |              |
     | #-------------------------#   #-------------------------# |    open source|  proprietary |
     |                                                           |    less sticky|       sticky |
     | #-------------------------#   #-------------------------# |    less mature|       mature |
     | |[d]                      |   |[e]                      | |               |              |
     | |       Jenkins X         |   |     Kafka operator      | |               |              |
     | |                         |   |                         | |               |              |
     | #-------------------------#   #-------------------------# |              -#              |
     |                Any managed Kubernetes service             |                   -#         | 
     #-----------------------------------------------------------#                    #---------' 
                                                                                     -#

[w]: {"a2s:delref": true, "fill": "#fff", "fillStyle": "solid"}
[p]: {"a2s:delref": true, "fill": "#ef5ba1", "fillStyle": "solid", "strokeStyle": "#000"}
[b]: {"a2s:delref": true, "fill": "#f99c41", "fillStyle": "solid", "strokeStyle": "#000"}
[d]: {"a2s:delref": true, "fill": "#27bdce", "fillStyle": "solid", "strokeStyle": "#000"}
[e]: {"a2s:delref": true, "fill": "#00aa5b", "fillStyle": "solid", "strokeStyle": "#000"}
```

```{=html}
<aside class="notes" data-markdown>
```
```{=html}
</aside>
```
<!-- section 27 -->

# CONFIGURATION {#configuration bg="#97dce7"}

``` {.render_a2sketch}
     #-----------------------------------------------------------#                                    -#
     |[w]                                                        |                    -#               |
     | #-------------------------#   #-------------------------# |                     |               |
     | |[p]                      |   |[b]                      | |                     |               |
     | |     Azure Key Vault     |   |       Cosmos DB         | |                     |               |
     | |                         |   |                         | |                     |               |
     | #-------------------------#   #-------------------------# |     -#              |               |
     |           #----------------------------------#            |      |              |               |
     |           |[w]                               |            | RBAC |  IAM         |               |
     |           |              AKS                 |            | CNI  |  NSGs & FWs  |  Terraform    |
     |           |                                  |            | CSI  |  Blob/Block/ |  (1000+ lines)|
     |           #----------------------------------#            |      |        Files |               |
     | #-------------------------#   #-------------------------# |     -#              |               |
     | |[d]                      |   |[e]                      | |                     |               |
     | |      Azure DevOps       |   |   Azure Queue Storage   | |                     |               |
     | |                         |   |                         | |                     |               |
     | #-------------------------#   #-------------------------# |                     |               |
     |                           Azure                           |                    -#               |
     #-----------------------------#-----------------------------#                                    -#
            Infrastructure as CODE | 
                                   |
                                   |
                                   |
                                   v Infrastructure as DATA       
     #-----------------------------#-----------------------------#                    -#
     |[w]                                                        |     -#              |
     | #-------------------------#   #-------------------------# |      |              |
     | |[p]                      |   |[b]                      | |      |              |
     | |     Vault operator      |   |   PostgreSQL operator   | |      |              |
     | |                         |   |                         | |      |              |
     | #-------------------------#   #-------------------------# | RBAC |              |
     |                                                           | CNI  |  Terraform   |
     | #-------------------------#   #-------------------------# | CSI  |  (100+ lines)|
     | |[d]                      |   |[e]                      | |      |              |
     | |       Jenkins X         |   |     Kafka operator      | |      |              |
     | |                         |   |                         | |      |              |
     | #-------------------------#   #-------------------------# |      |              |
     |                Any managed Kubernetes service             |     -#              |
     #-----------------------------------------------------------#                    -#

[w]: {"a2s:delref": true, "fill": "#fff", "fillStyle": "solid"}
[p]: {"a2s:delref": true, "fill": "#ef5ba1", "fillStyle": "solid", "strokeStyle": "#000"}
[b]: {"a2s:delref": true, "fill": "#f99c41", "fillStyle": "solid", "strokeStyle": "#000"}
[d]: {"a2s:delref": true, "fill": "#27bdce", "fillStyle": "solid", "strokeStyle": "#000"}
[e]: {"a2s:delref": true, "fill": "#00aa5b", "fillStyle": "solid", "strokeStyle": "#000"}
```

```{=html}
<aside class="notes" data-markdown>
```
This is the crux of the matter. So far from introducing additional complexity, the operator approach promises to reduce complexity dramatically.

This is arguably far more valuable than the reduction in cloud stickiness and lock-in, which is often the main or even sole argument put forward - after all, many companies are happy to commit to a single cloud vendor for now.
```{=html}
</aside>
```
<!-- section 28 -->

# NATIVE RESOURCES {#native-resources bg="#97dce7"}

``` {.render_a2sketch}
#---------------------------------------------------------------------#
|[q]                                                                  |
|                                                                     |
|                                                                     |
|  Can I trust custom resources to create and manage the lifecycle    |
|                                                                     |
|  of objects native to the platform?                                 |
|                                                                     |
|                                                                     |
|                                                                     |
#---------------------------------------------------------------------#

            #---------------------------------------------------------------------#
            |[a]                                                                  |
            |                                                                     |
            |                                                                     |
            |  Yes, this is something resources like PersistentVolumeClaim and    |
            |                                                                     |
            |  Service have done for a long time, dynamically creating storage    |
            |                                                                     |
            |  volumes and load balancers respectively.                           |
            |                                                                     |
            |                                                                     |
            |                                                                     |
            #---------------------------------------------------------------------#     


[q]: {"a2s:type": "quote-sw", "a2s:delref": true, "fill": "#ef5ba1", "fillStyle": "solid"}
[a]: {"a2s:type": "quote-se", "a2s:delref": true, "fill": "#6a2469", "fillStyle": "solid"}
```

<!-- section 29 -->

# SERVICE LEVEL {#service-level bg="#97dce7"}

``` {.render_a2sketch}
#---------------------------------------------------------------------#
|[q]                                                                  |
|                                                                     |
|                                                                     |
|  Can the PostgreSQL operator match the availability and durability  |
|                                                                     |
|  guarantees of managed SQL Server DBs?                              |
|                                                                     |
|                                                                     |
|                                                                     |
#---------------------------------------------------------------------#     

            #---------------------------------------------------------------------#
            |[a]                                                                  |
            |                                                                     |
            |                                                                     |
            |  Not today, no. It is worth considering, though, that:              |
            |                                                                     |
            |  * RDS and the operator use the same Azure storage primitives       |
            |                                                                     |
            |  * Until this improves, there's Microsoft's Azure Service Operator  |
            |    for Kubernetes (EventHub, Azure SQL, CosmosDB, Storage Accounts) |
            |                                                                     |
            |                                                                     |
            |                                                                     |
            #---------------------------------------------------------------------#     

[q]: {"a2s:type": "quote-sw", "a2s:delref": true, "fill": "#ef5ba1", "fillStyle": "solid"}
[a]: {"a2s:type": "quote-se", "a2s:delref": true, "fill": "#6a2469", "fillStyle": "solid"}
```

::: {.tiny}
Source: `<a href="https://cloudblogs.microsoft.com/opensource/2020/06/25/announcing-azure-service-operator-kubernetes/">`{=html}cloudblogs.microsoft.com/opensource/2020/06/25/announcing-azure-service-operator-kubernetes/`</a>`{=html}
:::

<!-- section 30 -->

# A PLAUSIBLE FUTURE, BUT NOT A DONE DEAL {#a-plausible-future-but-not-a-done-deal bg="#97dce7"}

``` {.render_a2sketch}
                                    Two choices: Crunchy and Zalando's Spilo
The CoreOS Vault operator depends   MySQL has a first-party operator by Oracle
on their etcd operator              There is also CNCF graduate project Vitess
             |                                           |
     #-------+-------------------------------------------+-------#
     |[w]    |                                           |       |
     | #-----+-------------------#   #-------------------+-----# |      
     | |[p]                      |   |[b]                      | |    
     | |     Vault operator      |   |   PostgreSQL operator   | |     
     | |                         |   |                         | |    
     | #-------------------------#   #-------------------------# |     
     |                                                           |    
     | #-------------------------#   #-------------------------# |     
     | |[d]                      |   |[e]                      | |    
     | |       Jenkins X         |   |     Kafka operator      | |      
     | |                         |   |                         | |     
     | #-----+-------------------#   #-------------------+-----# |     
     |       |        Any managed Kubernetes service     |       |     
     #-------+-------------------------------------------+-------#     
             |                                           |   
Note that this is not "Hudson"       First-party operator by Confluent
UI requires VMware Octant with       One promising alternative is the
octant-jx plugin                     RabbitMQ Cluster Operator

[w]: {"a2s:delref": true, "fill": "#fff", "fillStyle": "solid"}
[p]: {"a2s:delref": true, "fill": "#ef5ba1", "fillStyle": "solid", "strokeStyle": "#000"}
[b]: {"a2s:delref": true, "fill": "#f99c41", "fillStyle": "solid", "strokeStyle": "#000"}
[d]: {"a2s:delref": true, "fill": "#27bdce", "fillStyle": "solid", "strokeStyle": "#000"}
[e]: {"a2s:delref": true, "fill": "#00aa5b", "fillStyle": "solid", "strokeStyle": "#000"}
```

<!-- section 31 -->

# WHAT'S IN IT FOR US? {#whats-in-it-for-us bg="#fff44d"}

As with multicloud, the value proposition for the consumer can seem lacklustre, `<br/>`{=html}but there are tangible benefits

Create one path to production for all workloads (not three separate ones for containers, functions and VMs)

Enabling zero trust and mutual TLS is much easier, and again you only do it once

Continuous reconciliation based on policies you define beats defining desired state at the start and hoping for the best

<!-- section 32 -->

# SUMMARY {#summary .light-on-dark bg="#6a2469"}

Persistent cloud storage is just as reliable when claimed by a pod

The core Kuberenetes interfaces will continue to mature because everyone in the industry has a stake in it

The operator pattern is set to thrive because software companies and second-tier cloud vendors depend on it

Of all the large, distributed systems found in modern application architectures, only Kubernetes promises a significant reduction in complexity in return

<!-- section 33 -->

# THANK YOU {#thank-you .light-on-dark bgcss="tw-colorful"}

Slides built with `<a href="https://github.com/arnehilmann/markdeck">`{=html}Markdeck`</a>`{=html}`<br/>`{=html}
GitHub `<a href="https://github.com/gerald1248/stateful-kubernetes-slides">`{=html}gerald1248/stateful-kubernetes-slides`</a>`{=html}`<br/>`{=html}
Twitter `<a href="https://twitter.com/03spirit">`{=html}@03spirit`</a>`{=html}`<br/>`{=html}

`<img src="assets/img/ThoughtWorks_logo_white.png" width="200" />`{=html}
